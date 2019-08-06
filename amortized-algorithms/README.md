# Amortized Algorithms

Used when we are interested in performing a sequence of operations on a data structure.  We aren't particularly interested in the cost of a single operation, we want to know how bad how much the entire set will cost instead. 

## Worst Case Sequence Complexity

The worst case sequence complexity of _m_ operations is the maximum time over **all** sequences of $$m$$  
 operations.  

worst case sequence complexity  &lt;= $$m$$ \* worst case time complexity of any single operation in any sequence of $$m$$ operations.

### Examples

#### Hash table sizing.  

When we created a hash table we start by deciding how many slots we need.  If we make it too small, then we run out of space \(on chaining it leads to long chains, with open addressing we don't have any room to add anything\).  If we make it too big we waste memory.  So how do we address this?

We can add a "grow\(\)" function to the hash table.  Once the load factor hits a certain amount, grow\(\) the hash table.  What does grow\(\) involve?

* make new array that is twice as big as it was $$(m_{new} = 2 m)$$
* hash everything from old array into new array
* cost is n because every item in old array must be rehashed.

We then adjust the insert\(\) function to do following:

* check load factor, if it hits a certain threshold \(say n/m &gt; 0.5... this would be half full which is a good value to use for open addressing hash tables\), grow\(\)
* insert item \(into the new bigger table\)

Now...this sounds super expensive.  it means that our insertion is no longer constant.  Potentially there is an insertion that has a linear cost with respect to the number of items in the table.  However, how often does this actually occur?  How much does it actually cost when it does?

So firstly, we are not growing with every operation.  Consider a standard hash table with operations to insert\(\), search\(\),  and remove\(\) records.  Of these only insert\(\) could cause the hashtable to grow.   Insert\(\) only grows the hash table if a particular load factor is reached.  Thus, a hash table that doesn't need to grow won't.   Furthermore... what is the actual cost of grow\(\)?  grow\(\) does not always cost same amount because the hashtable is not the same size throughout.  So for example if the there were only two records in the hash table, then you only need to rehash two records....the "n" that grow\(\) costs is not the same n each time you call grow\(\).  Early on, its less expensive because there are less records, later it is more expensive.  Thus, we should not think of it as being the same throughout

#### Binary Counter

Suppose you had a binary counter with k bits \(think of it like an odometer with only 0's and 1's\).  The binary counter only has the **increment\(\)** operation which increases the counter by 1.  We define the cost as the number of bits flipped during an **increment\(\)** operation.  What is the cost per operation?

## 









