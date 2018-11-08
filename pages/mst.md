# Minimum Spanning Tree (MST)

### Purpose
Find the smallest path that connects all nodes in an 
undirected graph with positive edge weights to each other.

### Summary
A spanning tree is a subgraph that is a tree and connects all
nodes in the graph to each other. A cut is a partition of 
the graph's vertices into two non-empty sets. A crossing edge
connects a vertex in one set with a vertex in another.

The greedy algorithm solution says that given any cut, the 
crossing edge of min weight is in the MST. Kruskal, Prim, and 
Boruvka algorithms all do the greedy algorithm differently.

# Kruskal's Algorithm

### Summary
Use a queue, minimum priority queue, and union find to find
the MST. Consider edges in ascending order of weight. Add the
next edge to the MST unless doing so would create a cycle.
Uses all vertices connected to the vertex as the cut.

Computes MST in ElogE time (E == num edges).

# Prims Algorithm (lazy)

### Summary
Use a queue, minimum priority queue, and array to find the
MST. Start at vertex, add the vertex to the MST. Add all
adjacent edges with a vertex not in the tree to the
priority queue. Take the next vertex, repeat.

Run time is ElogE with extra space proportional to E
