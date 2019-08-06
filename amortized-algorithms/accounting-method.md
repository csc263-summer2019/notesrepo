# Accounting Method

The accounting method effectively charges for each operation, storing up credits so that later it can be used to pay for future operations.

Consider a the implementation of an array with two basic operations:

* append\(x\) - adds x to first free spot
* delete\(\) - removes item from last occupied spot

\(see arraystack implementation in course repo\).

If we allocate too much space for this array, we waste space.  If we allocate too little space we run out.  Similar to hash table problem. Thus what we do is that after we fill up the array, create a new array with double the capacity, copy everything over 

Firstly, because only append\(x\) grows the array, we will look at only performing append\(x\) operations.  Using the accounting method, we want to charge some amount for each operation in order to pay for future operations.



