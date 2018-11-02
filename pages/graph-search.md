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
from point A to point B (solving mazes). 

### Summary
It starts at the source node and recursively visits every connected 
node. Along the way, it also keeps track of the last element that 
it visited before arriving at the node (in the `edgeTo` array below)

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
  
  pathTo(vertex) {
    if (!hasPathTo(vertex)) { return null; }

    path = [];
    for (int i = vertex; i !== this.source; i = edgeTo[i]) {
      path.push(i);
    }
    path.push(this.source);
    return path;
  }
}
```

# Breadth First Search (BFS)

### Purpose
Breadth first search is good at figuring out the shortest path
from point A to point B.

### Summary
Uses a queue structure. Until the queue is empty, it removes a 
vertex from the queue, then adds to the queue all unmarked vertices
adjacent to this queue. As it touches each vertex, it marks it as
visited.

```javascript
class BreadthFirstPaths {
  constructor() {
    this.marked = [];
    this.edgeTo = [];
  }

  bfs(graph, source) {
    let queue = [];
    queue.unshift(source);
    this.marked[source] = true;

    while (queue.length !== 0) {
      let vertex = queue.shift();
      graph.graph[vertex].forEach(w => {
        if (!this.marked[w]) {
          queue.unshift(w);
          this.marked[w] = true;
          this.edgeTo[w] = vertex;
        }
      })
    }
  }
}
```


# Connected Components

### Purpose
Easily discover whether two vertices are connected. 

### Summary
Initialize all vertices as unmarked / unvisited. For each unmarked
vertex, run DFS to discover all vertices in the same connected
component. Store the id for this component with the vertex so that
you can quickly look up whether two things have the same component id,
and therefore, if they are connected.

```javascript
class ConnectedComponents {
  constructor(graph, source) {
    this.graph = graph;
    this.visited = [];
    this.connectedComponents = [];
    this.count = 0;

    for (i = 0; i < graph.length; i++) {
      if (!this.visited[i]) {
        this.dfs(i);
        this.count++;
      }
    }
  }

  dfs(source, id) {
    this.visited[source] = true;
    this.connectedComponents[source] = this.count;

    this.graph[source].forEach(v => {
      if (!this.visited[v]) {
        this.dfs(v);
      }
    })
  }

  count() {
    return this.count;
  }

  id(v) {
    return this.connectedComponents[v];
  }
}
```
