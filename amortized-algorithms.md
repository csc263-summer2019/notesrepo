# Amortized Algorithms

Used when we are interested in performing a sequence of operations on a data structure.  We aren't particularly interested in the cost of a single operation, we want to know how bad how much the entire set will cost instead. 

## Worst Case Sequence Complexity

The worst case sequence complexity of _m_ operations is the maximum time over **all** sequences of m operations.  

worst case sequence complexity  &lt;= m \* worst case time complexity of any single operation in any sequence of m operations.

### Examples

Hash table sizing.  When we created a hash table we start by deciding how many slots we need.  If we make it too small, then we run out of space \(on chaining it leads to long chains, with open addressing we don't have any room to add anything\).  If we make it too big we waste memory.  So how do we address this?

add a "grow\(\)" function to the hash table.  Once the load factor hits a certain amount, grow\(\) the hash table.  What does grow\(\) involve?

* make new array that is twice as big as it was $$(m_{new} = 2 m)$$
* hash everything from old array into new array
* cost is n because every item in old array must be rehashed.

We then adjust the insert\(\) function to do following:

* check load factor, if it hits a certain threshold \(say n/m &gt;= 0.5... this would be half full which is a good value to use for open addressing hash tables\), grow\(\)
* insert item \(into the new bigger table\)

Now...this sounds super expensive.  it means that our insertion is no longer constant.  Potentially there is an insertion that has a linear cost with respect to the number of items in the table.





