# Priority Queues

The binary heap is a data structure that can be used to implementation of a _**priority queue**_**.** Normally, when you have a queue, the first value in is the first value out. However with a _**priority queue**_ the value that comes out of the queue next depends on the priority of that value.

A _**priority queue**_ is an abstract data type.  Like queues and stacks, it is an idea, the underlying storage and access is decoupled from the functionality of a priority queue.  A priority queue is similar to a queue in that you use it for ordering data. However, instead of ordering based on when something was added, you order it based on the priority value of the item.  An item at the front of the priority queue \(and the item that will be removed if an item is to be dequeued\)  is the item with the highest priority.  This is the type of queues you might find in a hospital emergency room.  The thing that matters more is the severity of the illness as opposed to who got there first. 

Consider how you might try to implement such a queue and some of the operations you might wish to perform:

* insert - add an item to the queue
* delete - removes the item with the highest priority
* front - return the highest priority item in the queue

How would you go about implementing such an abstract data type?

If you were to implement a priority queue using a regular list you would essentially have to maintain a sorted list \(sorted by priority\). This would mean the following:

1. insertions would be O\(n\) for sure as you would need to go through an already sorted list trying to find the right place then do the insertion
2. removal is from the "front" of the queue, so depending on how you do your implementation, this can be potentially O\(n\) also.

This is not very efficient. If we were to create our priority queue in this manner the run time for both operations would not be very good.  Thus, clearly this isn't how we should implement a priority queue.

The interesting thing about a priority queue is that we really don't care where any value other than the one with the highest priority is. We care about where the highest priority item is and we want to be able to find it and remove it quickly but all other values can be essentially anywhere.

A binary heap is a data structure that can help us achieve this.



