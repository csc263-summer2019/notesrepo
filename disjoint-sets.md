# Disjoint Sets

The disjoint set $$S$$is a set of non-empty sets = $$ \{S_1, S_2, S_3...S_k\}$$ where no member of $$S_i$$ exist in any other set $$S_j$$,where $$ i\neq j$$.  That is, $$S_i$$and $$S_j$$ have no members in common.  Each set has an unique identifying member called the _representative_

With the ADT for organizing disjoint sets we aren't really interested in the elements within each set, just the sets themselves.

## Disjoint Set Operations

| Operation Name | Description |
| :--- | :--- |
| MakeSet\(x\) | given an element x that is not in any set, make a new set with x as its only element |
| FindSet\(x\) | given x, return the representative member of the set containing x |
| Union\(i,j\) | Given two sets with representatives i and j, form a new set that consists of $$S_i \cup S_j$$, and remove both $$S_i$$and $$S_j$$from the set \(leaving only the new unioned set\) .  We pick a new representative element from this union.  We can do this by using one of the original representatives of $$S_i$$or $$S_j$$though we don't have to do it this way. |

## Use Case

Why would we want such a data structure?  Sometimes we want to divide a set of elements into distinct groups.  This data structure helps to do this.  For example, we may have a graph made of a set of vertices and edges.  \(we will look at graphs later\).  Here is a picture for now of what we are talking about

What we want to know about the graph above is which of the vertices are connected together.  Now, visually this might be very easy for us to see, but computers don't store pictures.Instead something like the above is stored like this \(more on this later... this is just showing why we can't just "see" what isn't connected\):

So when given a data structure like the above, how do we figure out what is connected to what?

### Algorithm:

```text
Graph G;   // given a graph
           // We have some method of iterating through all the vertices
           //and edges.
DisjointSet S;   //begin with empty set
for each vertex v in G{
         S.makeSet(v);  //each vertex is placed into its own set
}
//edge e connects v1 and v2
for each edge e=(v1,v2) in G{
           //find the representatives of the set where 
           //v1 and v2 exist and use it to union the sets together
           S.union(S.findSet(v1),S.findSet(v2));
}
```

### What is the cost of the above?

Firstly it should be noted that what we are effectively doing is this:

* call makeSet\(\) \|V\| times
* call Union\(\) \|E\| times
* call findSet\(\) 2\|E\| times \(two for each union\)

We are not particularly interested in the cost of a single operation of Union\(\) or findSet\(\).  Instead we are more interested in the cost of how much it would cost in total for the entire sequence of m operations needed to create the disjoint set.

#### Worst case sequence of operations.

### Idea 1: Circular linked lists

* create a circular linked list.  As list is circular, instead of keeping pointer to first node keep pointer to last node \(last-&gt;next\_  is first node\).
* insertions at front/back are both O\(1\).
* use last node as representative
* animation of a circular linked list using just a single last pointer: [http://cathyatseneca.github.io/DSAnim/web/singlylinked.html](http://cathyatseneca.github.io/DSAnim/web/singlylinked.html)

#### Cost:

* makeSet\(x\) - O\(1\) - create linked list with just one node
  * When we create a set, we return the node containing x to the application so that it can be stored and quickly retrieved.  We assume that the cost of getting to the node containing x is constant as we can access that data via the application directly.
* Union\(i,j\) - "append" list j to list i.  O\(1\) .  This involves doing the following:
  * make end of j point to front of i
  * make end of i point to front of j
  * make last\_ the end of j   //sort of optional as the whole thing is circular...
* findSet\(x\) - traverse list till you find the last node.  Potentially this will require traversing the entire list.  $$\theta(length of linked list)$$

### Idea 2: linked list with back pointer as well as a pointer to rep in each node

* create a linked list with both a back and front pointer
* insertions at front/back are both O\(1\).
* use first node as representative
* have each node store an extra pointer to the first node.

#### Cost:

* makeSet\(x\) - O\(1\) - create linked list with just one node. 
* findSet\(x\) - O\(1\) - follow pointer from node to its rep
* Union\(i,j\) - append j to i.  The appending part is easy... and is O\(1\).  However, the nodes in the second list is not pointing to correct rep.  Go through second list and make it point to the new rep





Now... what is the cost of the above algorithm?

* call make set$$|V|$$ times.
* we have to call union\(\)  $$|E|$$times.
* each time we call union we have to call findSet\(\) twice $$ 2(|E|)$$

Note that the above are just function calls... we need to account for the cost of each call.  We aren't interested in the run time of a single call to findSet\(\), makeSet\(\) or union\(\).   Now.. how long it takes for each individual operation depends on things like how we represent our disjoint sets, how many elements are in each of the disjoint sets etc.  So lets suppose we can come up with the worst case run time for each of these based on how many elements are in each of the sets... but is the cost actually that that bad?  Suppose we need to perform m operations in total \(for above m = \|V\|+3\|E\|\).  We can find the worst case run time for each of the above functions then multiply it by m.  

But... that is actually an over estimate of the cost.  In the case of the above, we actually don't really care about the cost of a single operation.  What we want to know is given a sequence of operation, what is the total cost of creating the disjoint set?



   









