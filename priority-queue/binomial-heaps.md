# Binomial Heaps and Binomial Trees

Another data structure that could be used to implement a priority queue is a binomial heap.  The advantage of a binomial heap is that it supports the _**union**_ operation which combines two binomial heaps into one in $$O(log n)$$ .  While it is possible to write the _**union**_ operation using a binary heap, the run time of the operation would be  $$\theta(n)$$  \(append one array to the other then perform heapify on the array\).  

A _**binomial heap**_ is a collection \(forest\) of _**binomial trees**_**.**  In the discussion below, we will be building a min-heap \(smaller value, higher priority\).  You can do exactly the same operations for a max-heap, the difference is just what is considered to be higher priority

## **Binomial Trees**

 A binomial tree $$B_k$$is an ordered tree where

* $$B_0$$ is a tree with exactly one node
* $$B_k$$ is made of two binomial trees $$B_{k-1}%$$ that are linked such that the root of one tree is the left most child of the root of the other tree.

![](../.gitbook/assets/binomialheaps1.png)

A binomial tree $$B_k$$has 4 properties:

1. there are $$2^k$$nodes in $$B_k$$
2. the height of $$B_k$$is $$k$$
3. there are exactly $$k \choose i $$nodes at depth i \(where root is at depth 0\)

   ![](../.gitbook/assets/binomialheap2.png)

4. the root degree k.  for the children of the root you will find that their degree is k-1, k-2, ... 

   ![](../.gitbook/assets/binomialheap3.png)

## Binomial Heaps

A binomial heap is a collection of binomial trees that meet the following criteria:

1\) The values within each binomial heap follow the min-heap order property.  That is the parent of a node must not be smaller than the child of the node

2\) There can be only one tree of any degree within the heap \(as viewed from its root node\)

A binomial heap of with n nodes will support the following operations \(with the run times given\):

* Make-Heap - $$\theta(1)$$ - makes an empty heap
* Minimum\(\) - $$O(log n)$$returns the smallest item in the heap
* Union - $$O(log n)$$merges two heaps together into one heap
* Insert \(x\) - $$O(log n)$$ - inserts x into the heap
* Extract Minimum - $$\theta(log n)$$removes the smallest item from the heap

### Representation

To represent a binomial heap, we use a linked structure of nodes.

Each node will store the following:

* _**key**_ - the value stored in the heap.  The value we use to determine priority
* _**degree**_ - number of children the node has
* _**parent**_ - pointer to parent of the node, nullptr if node is root
* _**child**_ - pointer to leftmost child of node, nullpointer if node is leaf
* _**sibling**_ - pointer to the node just right of the current node nullptr if node is right most

Essentially at each level of the tree, you have a linked list from left to right.  the parent only points to the left most node of the tree

The heap itself consists of a head pointer that links to the lowest degree tree.  The trees are then linked by the root nodes \(using the sibling pointer\) of the binomial trees of the heaps.  The trees are ordered by the degree of the root \(in increasing order\)

### Make-Heap

Set head pointer to nullptr

### Minimum

Minimum value of heap must be in root node of one of the trees as each tree maintains min-heap order.  All we need to do is 

* start at the root of the first tree. make it's value current min.
* Follow the sibling pointer until the end, if any of the roots have the smallest value then it becomes the min.

Thus the number of binomial trees in the heap dictate how long this would take.  At most there are $$\lfloor {log n} \rfloor + 1$$ trees

### Union

The union operation merges together two binomial heaps.

We begin with two heaps \(called $$H_1$$and $$ H_2$$\).  In each heap there are different number of binomial trees of varying degrees ordered with lowest degree first.

Starting with the first tree in each of the heaps.  Two things can happen:

lowest degree is different - Select the tree with the lower degree for the final heap.  advance to next tree within the heap the tree came from

lowest degree is the same - Combine the two trees into one.  Remember that $$B_k$$is made of two trees that are both $$B_{k-1}$$.  Each of these two trees are already properly ordered as min-heaps.  Thus all we need to do is compare the roots.  Whichever value is smaller becomes the root of the combined tree and the other becomes that trees left most child.

At worst, we will end up needing to combine 3 trees of the same degree \(2 from the original tree, plus one more created as a result of merging two previous trees\).  

### Insert

Insert begins by creating adding a single node into the Heap \(A $$B_0$$tree\).  If there are no other $$B_0$$ trees we are done.  If there are, we combine the trees \(like just like the union algorithm\) forming a $$B_1$$tree.  We continue to combine trees in this manner until we get a tree with a unique degree

### Extract Minimum

* Create an empty heap $$H'$$
* Find the smallest tree with the smallest root
* delete the root and place each of the children into the empty heap
* Merge the old heap with $$H'$$







