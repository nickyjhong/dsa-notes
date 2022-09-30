# Adjacency List
[⬅ Go Back to Home](../README.md)

[⬅ Go Back to Topic](/graphs.md)

## Notes
- Most data in the real-world tends to lend itself to sparser and/or larger graphs

## Code - Undirected Graph
### Full Code
```js
class Graph {
  constructor() {
    this.adjacencyList = {}
  }
  addVertex(vertex) {
    this.adjacencyList[vertex] = [];
  }
  addEdge(vertex1, vertex2) {
    this.adjacencyList[vertex1].push(vertex2)
    this.adjacencyList[vertex2].push(vertex1)
  }
  removeEdge(vertex1, vertex2) {
    this.adjacencyList[vertex1] = this.adjacencyList[vertex1].filter(v => v !== vertex2)
    this.adjacencyList[vertex2] = this.adjacencyList[vertex2].filter(v => v !== vertex1)
  }
  removeVertex(vertex) {
    while(this.adjacencyList[vertex].length) {
      const adjacentVertex = this.adjacencyList[vertex].pop()
      this.removeEdge(vertex, adjacentVertex);
    }
    delete this.adjacencyList[vertex]
  }
}
```
### Pseudocodes / Breakdown
#### **Add** a vertex
- Write a method called `addVertex`, which accepts a name of a vertex
- It should add a key to the adjacency list with the name of the vertex and set its value to be an empty array
  ```js
  addVertex(vertex) {
    this.adjacencyList[vertex] = [];
  }
  ```
#### **Add** an edge
- This function should accept two verticies, and we can call them vertex1 and vertex2
- The function should find in the adjacency list the key of vertex1 and push vertex2 to the array
- The function should find in the adjancecy list the key of vertex2 and push vertex1 to the array
- Don't worry about handling errors/invalid vertices
  ```js
  addEdge(vertex1, vertex2) {
    this.adjacencyList[vertex1].push(vertex2)
    this.adjacencyList[vertex2].push(vertex1)
  }
  ```
  #### **Remove** an edge
- This function should accept two verticies, and we can call them vertex1 and vertex2
- The function should reassign the key of vertex1 to be an array that does not contain vertex2
- The function should reassign the key of vertex2 to be an array that does not contain vertex1
- Don't worry about handling errors/invalid vertices
  ```js
  removeEdge(vertex1, vertex2) {
    this.adjacencyList[vertex1] = this.adjacencyList[vertex1].filter(v => v !== vertex2)
    this.adjacencyList[vertex2] = this.adjacencyList[vertex2].filter(v => v !== vertex1)
  }
  ```
  #### **Remove** a vertex
- The function should accept a vertex to remove
- The function should loop as long as there are any other vertices in the adjacency list for that vertex
- Inside of the loop, call our `removeEdge` function with the adjacency list for that vertex
- Delete the key in the adjacency list for that vertex
  ```js
  removeVertex(vertex) {
    while(this.adjacencyList[vertex].length) {
      const adjacentVertex = this.adjacencyList[vertex].pop()
      this.removeEdge(vertex, adjacentVertex);
    }
    delete this.adjacencyList[vertex]
  }
  ```