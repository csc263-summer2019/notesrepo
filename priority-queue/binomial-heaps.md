# Binomial Heaps

Another data structure that could be used to implement a priority queue is a binomial heap.  The advantage of a binomial heap is that it supports the _**union**_ operation which combines two binomial heaps into one in $$O(log n)$$ .  While it is possible to write the _**union**_ operation using a binary heap, the run time of the operation would be  $$\theta(n)$$  \(append one array to the other then perform heapify on the array\).  

## Binomial Trees and Binomial Heaps

A _**binomial heap**_ is a collection of _**binomial trees**_**.**  A binomial tree $$B_k$$is an ordered tree where

* $$B_0$$ is a tree with exactly one node
* $$B_k$$ is made of two binomial trees $$B_{k-1}%$$ that are linked such that the root of one tree is the left most child of the root of the other tree.



