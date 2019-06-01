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

However what if what we wanted to track a larger set of possible keys?  For example suppose we wanted to track the frequency of ascii digrams \(2 character combos\).  We would have 256\*256 = 65 536 ranging from 0 to 65 535.  Relatively speaking this is still a very small number of keys so we can use the same method.  Just need to convert each character to an index by doing something like c1\*256 + c2 where c1 and c2 are the ASCII encoding of the first and second characters of the digrams respectively





