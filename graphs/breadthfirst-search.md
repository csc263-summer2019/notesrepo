# Breadth-first Search

Breadth-first search \(BFS\) is a method of traversing a graph $$G=(V,E)$$ starting from a source $$ s \in V $$.   BFS starts from a source vertex $$s$$.  It will then _**visits**_ every vertex $$v$$ reachable from $$s$$  forming a BFS tree and thus finding paths from $$s$$ to $$v$$.  BFS visits nodes in order based on its distance from $$s$$.  That is, it will first visit all vertices that are directly connected to s then vertices that are two vertices away and so on.

To perform a BFS on a graph, we keep track of the status of each vertex with a colour:

* white - vertex is not yet discovered in any way
* gray - vertex is encountered but not yet explored
* black - vertex is explored

How these colour come into play will be clear once we look at the algorithm.

We are going to look at how a breadthfirst search will work using the following graph, starting using vertex A as our starting point.  the graph's adjacency matrix and adjacency list are also shown.

![](../.gitbook/assets/graph4.png)

To support a breadthfirst search, we will use a _**queue**_.  Recall that a queue is a FIFO data structure that supports 

* enqueue\(x\)  - adds x to the queue
* dequeue\(\) - removes oldest item from queue
* front\(\) - returns oldest item in the queue

All above operations can be implemented with an O\(1\) runtime with either array or linked list.





