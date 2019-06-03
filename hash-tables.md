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

Now, what if we wanted to count the frequency of every word \(defined as 1 or more alphanumeric characters separated by 1 or more non-alphanumeric characters\).  

What if it was bigger still?  What if instead of storing the frequency of letters, we wanted to store the frequency of words within a file \(defined as a string of alphanumeric characters separated by 1 or more non-alphanumeric characters\).  This could potentially be an infinitely large set of possible keys as there is no limit on the word length.  Even if we were to limit the number of characters to some maximum wordlength m?  If we did this, then for each character in the word there are 62 possibilities \(26 upper, 26 lower, 10 numeric\).  Thus, the number of possible keys length exactly m is 62^m.  It doesn't take a very large m before the number of possible words become too big to give each of them an element with an array \(our array would have to be huge\).

Note that most of these potential keys are not actually likely to exist in the text file.  Thus, we only need to store information about the words that actually do exist.  The solution to this problem is a hash table

A hash table is a table that holds a set of key-value pairs.    In the above example of storing frequencies of words, the key would be the word.  The value would be the frequency of the word within the text file.

A hash table uses a hash function to transform a key into a valid hash index.

That is hash\(k\) = hashindex

The hash function is deterministic.  That is if we give it the same key, the same hashindex is always returned.

A discussion of hash functions will be given a little later. 



Unlike the very first example where the array index matched the key, our array index won't and thus, we must store both the key and value together at each element.

The basic operations on hash table are:

* insert\(k, v\) - inserts the key-value pair k-v into the hash table
* delete\(k\) - finds and removes a key-value pair with a key matching k
* search\(k\) - finds and returns the value associated with key matching k

Each of these operations



The basics of hash tables are very simple but there are a number of problems that we must deal with

* what hash function do we use?
* what happens if two different keys get hashed into the same position \(collision\)

### The pigeon hole principle

Suppose you had n mailboxes and m letters where m &gt; n  \(more letters than mailboxes\).  If that is the case then at least one mailbox must contain 2 letters.    This is effectively what the situation is with our hash function and keys.  The number of mailboxes we have is n \(size of array\).  The total number of possible keys in $$U$$is bigger than n \(usually significantly bigger\).  Thus $$| U | > n$$.  What this means is that the hash function must return the same value for at least two different keys.

Suppose the hash table were to contain two distinct keys $$k_1$$and $$k_2$$.  A _**collision**_ occurs if $$hashfunction(k_1) == hashfunction(k_2)$$.  

Our implementation of hash tables therefore must be able to deal with collisions.

## Collision Resolution

## Chaining

At every location \(hash index\) in your hash table store a linked list of items. Some space will still be wasted for the pointers but not nearly as much as bucketing. Table will also not overflow \(ie no pre-defined number of buckets to exceed\). You will still need to conduct a short linear search of the linked list but if your hash function uniformly distributes the items, the list should not be very long

### Linear Probing

Both bucketing and chaining essentially makes use of a second dimension to handle collisions. This is not the case for linear probing. Linear Probing uses just a regular one dimensional array.

### Insertion

The insertion algorithm is as follows:

* use hash function to find index for a record
* If that spot is already in use, we use next available spot in a "higher" index.
* Treat the hash table as if it is round, if you hit the end of the hash table, go back to the front

Each contiguous group of records \(groups of record in adjacent indices without any empty spots\) in the table is called a cluster.

### Searching

The search algorithm is as follows:

* use hash function to find index of where an item should be.
* If it isn't there search records that records after that hash location \(remember to treat table as cicular\) until either it found, or until an empty record is found. If there is an empty spot in the table before record is found, it means that the the record is not there.
* NOTE: it is important not to search the whole array till you get back to the starting index. As soon as you see an empty spot, your search needs to stop. If you don't, your search will be incredibly slow

### Removal

The removal algorithm is a bit trickier because after an object is removed, records in same cluster with a higher index than the removed object has to be adjusted. Otherwise the empty spot left by the removal will cause valid searches to fail.

The algorithm is as follows:

* find record and remove it making the spot empty
* For all records that follow it in the cluster, do the following:
  * determine the hash index of the record
  * determine if empty spot is between current location of record and the hash index.
  * move record to empty spot if it is, the record's location is now the empty spot.







