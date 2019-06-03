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

However what if what we wanted to track a larger set of possible keys?  For example suppose we wanted to track the frequency of ascii digrams \(2 character combos\).  We would have 256\*256 = 65 536 ranging from 0 to 65 535.  Relatively speaking this is still a very small number of keys so we can use the same method.  Just need to convert each character to an index by doing something like c1\*256 + c2 where c1 and c2 are the ASCII encoding of the first and second characters of the digrams respectively.

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









