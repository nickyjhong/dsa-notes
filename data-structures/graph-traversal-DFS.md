# Graph Traversal Depth First Search

[⬅ Go Back to Home](../README.md)

[⬅ Go Back to Topic](/graphs.md)

## Notes
- No root to start at like a binary tree
- Explore as far as possible down one branch before "backtracking"
  - Need to decide order to traverse graph
  - Very important to remember where we've already visited so we don't revisit the same vertex repeatedly

## Recursive
### Code
```js
DFSRecursive(start) {
  const result = []
  const visited = {};
  const adjacencyList = this.adjacencyList
  
  function dfs(vertex) {
    if(!vertex) return null;
    visited[vertex] = true;
    result.push(vertex)
    adjacencyList[vertex].forEach(neighbor => {
      if (!visited[neighbor]) {
        return dfs(neighbor)
      }
    })
  }
  dfs(start)
  return result
}
```
### Pseudocode / Breakdown
- The function should accept a starting node
- Create a list to store the end result to be returned at the very end
- Create an object to store visited vertices
- Create a helper function which accepts a vertex
  - The helper  function should return early if the vertex is empty
  - The helper function should replace the vertex it accepts into the visited object and push that vertex into the result array
  - Loop over all of the values in the adjacencyList for that vertex
  - If any of those values have not been visited, recursively invoke the helper function with that vertex
- Invoke the helper function with the starting vertex
- Return the result array
```js
DFSRecursive(vertex):
  if vertex is empty
    return (this is base case)
  add vertex to results list
  mark vertex as visited
  for each neighbor in vertex's neighbors:
    if neighbor is not visited:
      recursively call DFS on neighbor
```

## Iterative
### Code
```js
DFSIterative(start) {
  let stack = [ start ]
  let result = []
  let visited = {}
  let currentVertex

  visited[start] = true;
  while(stack.length) {
    currentVertex = stack.pop()
    result.push(currentVertex);

    this.adjacencyList[currentVertex].forEach(neighbor => {
      if(!visited[neighbor]) {
        visited[neighbor] = true;
        stack.push(neighbor);
      }
    });
  }
  return result
}
```
### Pseudocode / Breakdown
- The function should accept a starting node
- Create a stack to help keep track of verticies (use a list/array)
- Create a list to store the end result to be returned at the very end
- Create an oject to store visited vertices
- Add the starting vertex to the stack and mark it visited
- While the stack has something in it:
  - Pop the next vertex from the stack
  - If that vertex hasn't been visited yet:
    - Mark it as visited
    - Add it to the result list
    - Push all of its neighbors into the stack
- Return the result array
```js
DFSIterative(start):
  let S be a stack
  S.push(start)
  while S is not empty
    vertex = S.pop()
    if vertex is not labeled as discovered:
      visit vertex (add to result list)
      label vertex as discovered
      for each of vertex's neighbors, N do 
        S.push(N)
```
