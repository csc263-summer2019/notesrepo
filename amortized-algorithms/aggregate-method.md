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

