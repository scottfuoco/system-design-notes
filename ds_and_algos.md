## Dynamic Programming

Dynamic programing problems are problems that can be reduced into smaller problems. The solutions
to those smaller problems can then be used to solve the larger/original question.

## Graphs

A graph is a network of nodes/vertices and edges connecting them.

adjacent nodes, are nodes with edges between them

a path between two nodes without repeating nodes

a cycle is a path that start and end at the same node, without repeats

paths are considered connected if they have at least one path between them

components are maximal grouping of nodes that are all connected

graphs can contain isolated nodes and components

## Directed Graphs

Strongly connected, if two nodes can reach each other. If node A can reach node B but B cannot reach A
in a directed graph then they are connected but not strongly connectly.

## Graph properties

Simple - no duplicate edges, no edges from a node to itself

Connected a graph has only 1 connected component. So evey node is connected to every other node

Complete every node is adjacent to each other

Acyclic graph has no cycles, aka a forest

## Storing Graphs in Code

Adjacency Matrix

a 2d array [A][b] that contains values about the edge of the index a,b.

A B C
A 0 1 1
B 1 0 0
C 1 1 0

This graph shows the edges for a graph. Undirectled graphs will have x,y = 1 and y,x = 1

Adjacency matrix are O(v^2) in size, making them not very useful

**Adjacency List**

A: [B, C]
B: [B]
C: [A, B]

Checking if two nodes are adjacent can be O(e), e = number of edges in the worst case or
O(loge) if you use a set, so the matix is better for edge detection

But the memory usage is O(v+e) which can be much better than a matrix, you can iterate over
all neighbours in O(# of neighbors) instead of O(v) in the matrix

Because of this it can work for almost all graph problems and is highly useful.
