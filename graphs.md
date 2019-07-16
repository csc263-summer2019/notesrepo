# Graphs

A Graph $$G=(V,E)$$ is made up made of a set of vertices $$V={v_1, v_2, v_3...}$$ and edges $$E ={e_1,e_2, e_3...}$$. Each edge in $$E$$ defines a connection between $$(u,v)$$, where $$u,v \in V$$

Here is a drawing of a graph:

 

![](.gitbook/assets/graph1.png)

This graph has vertices A, B, C, D, E, F and G.  Note that these are really just labels that can be used to refer to the vertices... in reality we don't necessarily store labels in this manner.  Often vertices are just numbered

Edges can also have weights

  

![Graph where edges have weights](.gitbook/assets/graph2.png)

The weights on an edge can act in a way to serve as information about the nature of the connection between two vertices.  For example, each vertex can represent a city and the weights, the distance between the cities.

Aside for weights, an edge may also include a direction.  Graphs where edges have directions are also called a digraph

![Graph where edges have weight and direction](.gitbook/assets/graph3%20%281%29.png)



## Representation <a id="representation"></a>

To store the info about a graph, there are two general approaches.

* Adjacency list
* Adjacency matrix

These can each have its own advantages and disadvantages:



