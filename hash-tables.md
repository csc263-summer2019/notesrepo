# Hash Tables

Suppose you wanted to track a set of key/value pairs. That is you want to be able insert/search/delete based on the key but it would return the associated value.  

How would this be accomplished?  Now, if the possible keys were small, you could create a lookup table.  For example, suppose you were trying to do something like tracking the frequency of characters in an ASCII based text file.  ASCII values range from 0 to 127, extended ascii from 0 to 255.    This is a relatively small set of keys.  We can simply associate each ascii value to an array subscript and store the frequency in the corresponding element.

Thus suppose your file said \(assuming there are no leading or trailing blanks\):

```text
The quick brown dog jumped over the lazy fox!
```

The table to store the frequencies would be an array of 256 unsigned integers.    Thus we would end up with:

```text
'T' is ASCII 84, table[84]=1
'h' is ASCII 104, table[104]=2
'e' is ASCII 101, table[101]=4
' ' (space) is ASCII 32, table[32]=8
...
etc
```

It would be very fast to look up/or update a frequency.  

However what if what we wanted to track a larger set of possible keys?  For example suppose we wanted to track the frequency of ascii digrams \(2 character combos\).  We would have 256\*256 = 65 536 ranging from 0 to 65 535.  Relatively speaking this is still a very small number of keys so we can use the same method.  Just need to convert each character to an index by doing something like $$c1(256) + c2$$ . where $$c1$$ and $$c2$$ are the ASCII encoding of the first and second characters of the digrams respectively. 

What if it was bigger still?  What if instead of storing the frequency of letters, we wanted to store the frequency of words within a file \(defined as a string of alphanumeric characters separated by 1 or more non-alphanumeric characters\).  This could potentially be an infinitely large set of possible keys as there is no limit on the word length.  Even if we were to limit the number of characters to some maximum wordlength m?  If we did this, then for each character in the word there are 62 possibilities \(26 upper, 26 lower, 10 numeric\).  Thus, the number of possible keys length exactly m long is $$62^m$$.  It doesn't take a very large m before the number of possible words become too big to give each of them an element within an array \(our array would have to be huge\).

Note that most of these potential keys are not actually likely to exist in the text file.  Thus, we only need to store information about the words that actually do exist.  The solution to this problem is a hash table

A hash table is a table that holds a set of key-value pairs.    In the above example of storing frequencies of words, the key would be the word.  The value would be the frequency of the word within the text file.

A hash table uses a hash function to transform a key into a valid hash index.

That is hash\(k\) = hashindex

The hash function is deterministic.  That is if we give it the same key, the same hashindex is always returned.  A discussion of hash functions will be given a little later. 

Unlike the very first example where the array index matched the key, our array index and keys will not match each other and thus, we must store both the key and value together at each element.

In general the hash table supports the following functions:

* insert\(k, v\) - inserts the key-value pair k-v into the hash table
* delete\(k\) - finds and removes a key-value pair with a key matching k
* search\(k\) - finds and returns the value associated with key matching k

To implement each of the above function, the general algorithm is:

* calculate $$i = hash(k)$$, $$i$$ is the hash index
* use $$i$$ to access $$array[i]$$and perform the necessary operation on array\[i\].
* For example if we called insert\(k,v\) we start by calculaing $$hash(k)$$.  This will produce a hashindex i.
* We then place $$(k,v)$$into $$array[i]$$.  

{% hint style="info" %}
Think of an operation as being performed on array\[hash\(k\)\] instead of using k directly as the index.
{% endhint %}

The basics of hash tables are very simple but there are a number of problems that we must deal with

* what hash function do we use?
* what happens if two different keys get hashed into the same position \(collision\)

### The pigeon hole principle

Suppose you had n mailboxes and m letters where m &gt; n  \(more letters than mailboxes\).  If that is the case then at least one mailbox must contain 2 letters.    This is effectively what the situation is with our hash function and keys.  The number of mailboxes we have is n \(capacity of array\).  The total number of possible keys is m.  Usually the total number of possible keys is bigger than the capacity of the array. \(usually significantly bigger\).  Based on the pigeon hole principle, what this means is that the hash function must return the same value for at least two distinct keys.

Suppose the hash table were to contain two distinct keys $$k_1$$and $$k_2$$.  A _**collision**_ occurs if $$hash(k_1) == hash(k_2)$$.  

Our implementation of hash tables therefore must be able to deal with collisions.

## Collision Resolution

Collision resolution is the process of dealing with collisions.  In general there are two forms general methods for dealing with collisions.  Closed Addressing and Open addressing. 

A closed addressing system, the key value pair $$(k,v)$$ must be stored at index $$hash(k)$$, while in open addressing systems we allow $$(k,v)$$ to be stored elsewhere \(but in a predictable manner\).  This next sections looks at how this is done.

### Closed Addressing - Chaining

Chaining is a simple way of handling collisions.  Instead of storing the key-value pair $$(k,v)$$ into the array directly, chaining creates an array of linked lists, initially all empty.  For each operation involving key $$k$$

* calculate  $$ i = hash(k) $$
* perform operation \(insert/delete/search\) on the linked list at array\[i\]

#### Example

Suppose we were to have 6 keys $$ (k_1, k_2, k_3, k_4,k_5, k_6)$$.  The hash function returns as follows for these keys:  $$(hash(k_1) == 0, hash(k_2) == m-3, hash(k_3) ==m-1, hash(k_4) == m-3, hash(k_5) == 0, hash(k_6) == m-3$$

A table created using chaining would store records as follows \(note that only key's are shown in diagram for brevity\)

![](.gitbook/assets/chaining1.png)

#### Worst case run time

_**insert\(k,v\)**_ - cost to find the correct linked list + cost to search for k within the linked list, + cost to add new node or modify existing if k is found

_**search\(k\)**_ - cost to find the correct linked list + cost to search for k within the linked list

_**delete\(k\)**_ - cost to find the correct linked list + cost to search for k within the linked list + cost to remove a node from list

In each of the above cases, cost of to find the correct linked list is $$ \theta(1) $$ assuming that the cost of calculating hash is constant relative to number keys.  We simply need to calculate the hash index, then go to that location

The cost to add a node, modify a node or delete a node \(once node has been found\) is $$\theta(1)$$ as that is the cost to remove/insert into linked list given pointers to appropriate nodes

The cost to search through linked list depends on number of nodes in the linked list.  At worst, every single key hashes into exactly the same index.  If that is the case, the run time would be $$\theta(n)$$

Thus,  the worst case run time is $$\theta(n)$$.  In reality of course, the performance is signficantly better than this and you typically don't encounter this worst case behaviour.  Notice that the part that is slow is the search along the linked list.  If our linked list is relatively short then the cost to search it would also not take very long.

#### Average case run time

We begin by making an assumption called Simple Uniform Hash Assumption \(SUHA\).  This is the assumption that any key is equally likely to hash to any slot. The question then becomes how long are our linked lists?  This largely depends on the load factor $$\alpha = n/m $$ where n is the number of items stored in the linked list and m is the number of slots.  The average run time  is $$\theta( 1 + \alpha)$$

 



## Open Addressing

With hash tables where collision resolution is handled via open addressing, each record actually has a set of hash indexes where they can go.  If the first location at the first hash index is occupied, it goes to the second, if that is occupied it goes to the third etc.  The way this set of hash indexes is calculated depends on the probing method used \(and in implementation we may not actually generate the full set but simply apply the probing algorithm to determine where the "next" spot should be\).  We will begin by discussing the general algorithm used then look at how the various probing methods generate the set of indices for.

###  Basic Storage

Due to way open addressing works and how we will eventually need to handle insertion, each array element not only must hold the key value pair but it must also hold a status.  The status of each slot is:

* empty - slot is empty, has never held any key-value pair, does not currently hold any record
* used - slot is currently in used.  It holds a key-value pair.  Do not put anything into a spot that is used
* deleted - slot use to hold a key-value pair but currently doesn't.  When we are looking for a record we need to continue searching when we see deleted slots \(more on this later\)

### Searching

_**search\(k\)**_

The search algorithm is as follows:

* use hash function to find index of where an item should be.
* Check to see if the item's key matches that of key we are looking for
* If it isn't there search for key-value pairs in the "next" slot according to the probing method until either it found, or until an we hit an empty slot.  Note that only empty slots stop searching not deleted slots
* NOTE: it is important **not** to search the whole array till you get back to the starting index. As soon as you see an empty slot, your search needs to stop. If you don't, your search will be incredibly slow for any item that doesn't exist.

### Insertion

_**insert\(k,v\)**_

The insertion algorithm is as follows:

* If it is not there, start looking for the first "open" spot. in the set of probed indices and place k,v there.  An open spot is the first probe index that is either deleted or empty.

### Removal

_**remove\(k\)**_

The removal algorithm is as follows:

* search for the record with matching key.
* If you find it, mark the spot as deleted

### Probing methods:

#### Linear probing

Linear probing is the simplest method of defining "next" index for open address hash tables.  Suppose hash\(k\) = i, then the next index is simply i+1, i+2, i+3, etc.  You should also treat the entire table as if its round \(front of array follows the back\). Suppose that m represents the number of slots in the table, We can thus describe our probing sequence as:  $$\{ hash(k), (hash(k)+1)\%m, (hash(k)+2) \% m, (hash(k)+3)\%m, \dots \} $$

#### Example of linear probing:

Suppose we the following 6 keys and their associated hash indices \(these are picked  so that collisions will definitely occur\).  Let us then insert these 5 keys from k1 to k5 in that order.  

| Key | Hash index |
| :--- | :--- |
| k1 | 8 |
| k2 | 7 |
| k3 | 9 |
| k4 | 7 |
| k5 | 8 |
| k6 | 9 |

Insert k1 to k3 \(no collisions, so they go to their hash indices\)

![Insert k1, then k2, then k3](.gitbook/assets/hash2.png)

Insert k4. probe sequence of k4 is $$\{ (7+0)\%10, (7+1)\%10 , (7+2)\%10, (7+3)\%10, (7+4)\%10, (7+5)\%10, \dots \} = \{7, 8, 9, 0, 1, 2 \dots \}$$.  Thus, we place k4 into index 0 because 7, 8 and 9 are all occupied

![Insert k4](.gitbook/assets/hash3.png)

Insert k5. probe sequence of k5 is $$\{ (8+0)\%10, (8+1)\%10 , (8+2)\%10, (8+3)\%10, (8+4)\%10, (8+5)\%10, \dots \} = \{8, 9, 0, 1, 2, 3 \dots \}$$.  Thus, we place k5 into index 1 because 8, 9 and 0 are all occupied

![Insert k5](.gitbook/assets/hash4.png)

Suppose we then decided to do a search.  First lets search for something that isn't there, k6.  k6's probe sequence is:  $$ \{ (9+0)\%10, (9+1)\%10 , (9+2)\%10, (9+3)\%10, (9+4)\%10, (9+5)\%10, \dots\ } = \{ 9, 0, 1, 2, 3, 4 \dots \}$$  is $$\{ (9+0)\%10, (9+1)\%10 , (9+2)\%10, (9+3)\%10, (9+4)\%10, (9+5)\%10, \dots \} = \{9, 0, 1, 2, 3, 4 \dots \}$$.  We begin looking at the first probe index.  We proceed until we get to index 2.  Since index 2 is empty, we can stop searching

![search for k6 \(not in table\)](.gitbook/assets/hash6.png)

If we were to search for something that is there \(k5 for example\), here is what we would do. Probe sequence for k5 is $$ \{8, 9, 0, 1, 2, 3 \dots \}$$.  Thus, we would start search at 8, we would look at indices 8,9,0, and 1.  At index 1 we find k5 so we stop

![Search for k5 \(in table\)](.gitbook/assets/hash5.png)

Suppose we delete k3.  All we need to do is find it, and mark the spot as deleted

![delete k3](.gitbook/assets/hash7.png)

When a spot is deleted, we still continue when we search... thus if we were to look for k5, we do not stop on deleted, we must keep going.

![search for k5 \(in table\)](.gitbook/assets/hash8.png)

#### Quadratic Probing

With linear probing everytime two records get placed beside each other in adjacent slots, we create a higher probability that a third record will result in a collision \(think of it as a target that got bigger\).  One way to avoid this is to use a different probing method so that records are placed further away instead of immediately next to the first spot.  In quadratic probing, instead of using  the next spot, we use a quadratic  formula in the probing sequence.  The general form of this algorithm for probe sequence i is: $$hash(k)+{c_1}i + {c_2}i^2$$.  At it's simplest we can use $$hash(k)+i^2$$.   Thus, we can use: $$\{ hash(k), (hash(k)+1)\%m, (hash(k)+4) \% m, (hash(k)+9)\%m, \dots \}$$

| Key | Hash index |
| :--- | :--- |
| k1 | 8 |
| k2 | 7 |
| k3 | 9 |
| k4 | 7 |
| k5 | 8 |
| k6 | 9 |

#### Quadratic Probing Example

Insert k1 to k3 \(no collisions, so they go to their hash indices\)

![Insert k1, then k2, then k3](.gitbook/assets/hash9.png)

Insert k4. probe sequence of k4 is $$\{ (7+0^2)\%10, (7+1^2)\%10 , (7+2^2)\%10, (7+3^2)\%10, (7+4^2)\%10, (7+5^2)\%10, \dots \} = \{7, 8, 1, 6, 3, 2 \dots \}$$.  Thus, we place k4 into index 1 because 7 and 8 are both occupied

![Insert k4](.gitbook/assets/hash10.png)

Insert k5. probe sequence of k4 is $$\{ (8+0^2)\%10, (8+1^2)\%10 , (8+2^2)\%10, (8+3^2)\%10, (8+4^2)\%10, (8+5^2)\%10, \dots \} = \{8, 9, 2, 7, 4, 3 \dots \}$$.  Thus, we place k5 into index 2 because 8 and 9 are both occupied

![Insert k5](.gitbook/assets/hash11.png)

Likewise searching involves probing along its quadratic probing sequence.  Thus, searching for k6 involves the probe sequence  $$\{ (9+0^2)\%10, (9+1^2)\%10 , (9+2^2)\%10, (9+3^2)\%10, (9+4^2)\%10, (9+5^2)\%10, \dots \} = \{9, 0, 3, 8, 5, 4 \dots \}$$.   We search index 9, then index 0.  We can stop at this point as index 0 is empty

![search for k6](.gitbook/assets/hash12.png)





#### Double Hashing

In double hashing we have 2 different hash functions, $$hash_1(k)$$and $$hash_2(k)$$.  We use the first hash function to determine its general position, then use the second to calculate an offset for probes.  Thus the probe sequence is calculated as: $$ \{ hash_1(k), (hash_1(k) + hash_2(k))\%m, (hash_1(k) + 2 hash_2(k))\%m,  (hash_1(k) + 3 hash_2(k))\%m, \dots \} $$



| Key | Hash1\(key\) | Hash2\(key\) |
| :--- | :--- | :--- |
| k1 | 8 | 6 |
| k2 | 7 | 2 |
| k3 | 9 | 5 |
| k4 | 7 | 4 |
| k5 | 8 | 3 |
| k6 | 9 | 2 |

Double uses a second hash function to calculating a probing offset.  Thus, the first hash function locates the record \(initial probe index\)... should there be a collision, the next probe sequence is a hash2\(key\) away.  

Again we start off with hashing k1, k2 and k3 which do not have any collisions

![Insert k1,k2 and k3](.gitbook/assets/hash14.png)

Insert k4. probe sequence of k4 is $$\{ (7+0 (4))\%10, (7+1(4))\%10 , (7+2(4))\%10, (7+3(4))\%10, \dots \} = \{7, 1, 5, 9,  \dots \}$$.  Thus, we place k4 into index 1 because 7 was occupied

![Insert k4, ](.gitbook/assets/hash15.png)

Insert k5. probe sequence of k5 is $$\{ (8+0 (3))\%10, (8+1(3))\%10 , (8+2(3))\%10, (8+3(3))\%10, \dots \} = \{8, 1, 4, 7,  \dots \}$$.  Thus, we place k5 into index 4 because 8 and 1 were occupied

![Insert k5](.gitbook/assets/hash16a.png)





