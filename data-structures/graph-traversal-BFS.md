# Graph Traversal Breadth First Search
[⬅ Go Back to Home](../README.md)

[⬅ Go Back to Topic](/graphs.md)

## Notes
- Prioritizes visiting neighbors at current depth first before descending 

## Code
```js
BFS(start) {
  const queue = [ start ];
  const result = [];
  const visited = {};
  let currentVertex;

  while(queue.length) {
    currentVertex = queue.shift();
    result.push(currentVertex);
    this.adjacencyList[currentVertex].forEach(neighbor => {
      if(!visited[neighbor]) {
        visited[neighbor] = true;
        queue.push(neighbor);
      } 
    })
  } 
  return result;
} 
```
### Pseudocode / Breakdown
- This function should accept a starting vertex
- Create a queue (you can use an ar ray) and place the starting vertex in it
- Create an array to store the nodes visited
- Create an object to store nodes visited
- Mark the starting vertex as visited
- Loop as long as there is anything in the queue
- Remove the first vertex from the queue and push it into the array that stores nodes visited
- Loop over each vertex in the adjacency list for the vertex you are visited
- If it is not inside the object that stores nodes visited, mark it as visited and enqueue that vertex
- Once you have finished looping, return the array of visited nodes