# Graph Search

### Purpose
Find connections / paths between elements

### Summary
A graph is a representation of the connections between some data. Below
is a representation of a graph using javascript. It is instantiated with
a number N vertices. Each vertex is represented by its index in the graph. 
Each vertex is associated with an array of other vertices it is connected
to (creating edges).

```javascript
class Graph {
  constructor(numVertices) {
    this.graph = {};
    this.vertices = numVertices;
    for (let i = 0; i < numVertices; i++) {
      this.graph[i] = [];
    }
  }

  addEdge(v, w) {
    this.graph[v].push(w);
    this.graph[w].push(v);
  }

  addVertex(v) {
    this.graph[v] = [];
  }
}
```

# Depth First Search (DFS)

### Purpose
Depth first search is good at figuring out whether there is a path
from point A to point B (solving mazes). It starts at the source
node and recursively visits every connected node. Along the way,
it also keeps track of the last element that it visited before
arriving at the node (in the `edgeTo` array below)

```javascript
class DepthFirstPaths {
  constructor(graph, source) {
    this.visited = [];
    this.edgeTo = [];

    this.dfs(graph, source);
  }

  dfs(graph, vertex) {
    this.visited[vertex] = true;
    graph.graph[vertex].forEach(v => {
      if (!this.visited[v]) {
        this.dfs(graph, v);
        this.edgeTo[v] = vertex;
      }
    })
  }

  hasPathTo(vertex) {
    return this.visited[vertex];
  }
}
```