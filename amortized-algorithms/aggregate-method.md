# Aggregate Method

With the aggregate method, we compute the worst case sequence complexity of a sequence of operations then divide by the the number of operations.

### Example 1: Binary Counter

Suppose you had a binary counter with k bits \(think of it like an odometer with only 0's and 1's\).  The binary counter only has the **increment\(\)** operation which increases the counter by 1.  We define the cost as the number of bits flipped during an **increment\(\)** operation. 

Consider the example with k = 6

| Operation | Value | Counter | Cost |
| :--- | :--- | :--- | :--- |
| Intial Value | 0 | 00 0000 | - |
| Increment\(\) | 1 | 00 0001 | 1 |
| Increment\(\) | 2 | 00 0010 | 2 |
| Increment\(\) | 3 | 00 0011 | 1 |
| Increment\(\) | 4 | 00 0100 | 3 |
| Increment\(\) | 5 | 00 0101 | 1 |
| Increment\(\) | 6 | 00 0110 | 2 |
| ... | ... | ... | ... |
| Increment\(\) | 61 | 11 1101 | 1 |
| Increment\(\) | 62 | 11 1110 | 2 |
| Increment\(\) | 63 | 11 1111 | 1 |
| Increment\(\) | 0 | 00 0000 | 6 |

It may not be clear how many bits are changed each time... but if you look at how often we change each bit, it will be a lot simpler:

| Bit number | how often it changes | Total changes over m operations |
| :--- | :--- | :--- |
| 0 | Every operation | $$m = \lfloor {m \over 1}\rfloor = \lfloor{m \over {2^0}}\rfloor$$ |
| 1 | every 2 operations | $$\lfloor {m\over 2}\rfloor = \lfloor {m\over 2^{1}}\rfloor$$ |
| 2 | every 4 operations | $$\lfloor {m\over4} \rfloor = \lfloor {m\over 2^{2}}\rfloor$$ |
| 3 | every 8 operations | $$\lfloor {m \over 8} \rfloor =\lfloor {m\over {2^3}}\rfloor$$ |
| .... | ... | ... |
| k-1 | every $$2^{k-1}$$operations | $$\lfloor  {{m} \over {2^{k-1}}}\rfloor$$ |

Thus, the number of bit changes over m operations is simply a sum of the number of bit changes of each of the bits:

$$\sum\limits_{i=0}^{k-1} {\lfloor {m \over {2^{i}}}\rfloor}<= m \sum\limits_{i=0}^{k-1} {1 \over {2^{i}}} <= m \sum\limits_{i=0}^{\infty} {1 \over {2^{i}}} <= 2m$$

Thus, the amortized cost is $${2m \over m } = 2$$ per increment\(\) operation.

### Hash Table Resizing

Going back to the hashtable resizing example.  We alter the insertion\(x\) function to something like:

```text
insert(x){
    if(loadFactor() >= 0.5){
        create new table with double the capacity
        go through current table, for every non-nil element
           rehash into new table
    }
    hashidx=hashfunction(x.key);
    place x into table[hashidx], handle collision as needed
}
```

For our purposes lets assume that except for the grow\(\) function, the rest of insertion\(\) is constant \(ie that our hash function will evenly distribute our data set evenly etc.\).  

Now..lets say that we perform m operations, if we only call insert\(\) then grow\(\) will be called more often.  Now, lets suppose we start with an array of capacity 2 holding 0 records.  Which insert\(\) operations call grow\(\) and how many elements are copied when it does?

| Operation | Number of elements | Capacity\(after\) | Load factor before | Load factor after | grow\(\)? |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Initial | 0 | 2 | 0 | 0 | - |
| insert\(\) | 1 | 2 | 0 | 0.5 | No |
| insert\(\) | 2 | 4 | 0.5 | 0.5 | Yes |
| insert\(\)  | 3 | 8 | 0.5 | 0.375 | Yes |
| insert\(\) | 4 | 8 | 0.375 | 0.5 | No |
| insert\(\) | 5 | 16 | 0.5 | 0.3125 | Yes |
| insert\(\)  | 6 | 16 | 0.3125 | 0.375 | No |
| insert\(\)  | 7 | 16 | 0.375 | 0.4375 | No |
| insert\(\) | 8 | 16 | 0.4375 | 0.5 | No |
| insert\(\) | 9 | 32 | 0.5 | 0.28125 | Yes |

Now.. if you take a look, we only grow at certain points.  we grow when i = 2,3,5, 9, ...17, 33 ... etc.

How many times does grow occur over m operations?  $$\lceil log m\rceil$$

now... each operation of grow\(\) though has a different cost because we are rehashing different number of elements?

| grow count | ith insertion | grow\(\) cost |
| :--- | :--- | :--- |
| 1st grow\(\) | 2 | 1 = $$2^0$$ |
| 2nd grow\(\) | 3 | 2 = $$ 2^1$$ |
| 3rd grow\(\)... | 5 | 4 = $$2^2$$ |
| 4th grow\(\) | 9 | 8 = $$2^3$$ |
| ... | ... | ... |

Thus, the cost of m insertion operations = cost of doing the insertion + cost of grow over m operations

$$m + \sum\limits_{i=0}^{\lceil logm \rceil} 2^i <= m + \sum\limits_{i=0}^{(logm) + 1} 2^i  = m + 2^{(logm) +2}-1= m + 2^(logm)(2^2) -1 = m + 4m -1=5m-1$$

