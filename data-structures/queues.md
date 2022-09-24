# Queues
[⬅ Go Back to Home](../README.md)

[⬅ Go Back to Topic](/stacks-queues.md)

## Notes
- **FIFO** - First In First Out
  - First element added to the queue will be the first element removed from the stack
    - Think of waiting in a line
- Where queues are used:
  - Background tasks
  - Uploading resources
  - Printing / Task processing

## Big O
- Time:
  - **Insertion - O(1)**
  - **Removal - O(1)**
  - Searching - O(n)
  - Access - O(n)

## Linked List Implementation
### Full Code
```js
class Queue {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }
}

class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
  enqueue(val) {
    const newNode = new Node(val);
    if (!this.first) {
      this.first = newNode;
      this.last = newNode;
    } else {
      this.last.next = newNode;
      this.last = newNode;
    }
    return this.size++;
  }
  dequeue() {
    if (!this.first) return null;
    let first = this.first;
    if (this.first === this.last) {
      this.last = null;
    }
    this.first = this.first.next;
    this.size--;
    return first.val;
  }
}
```
### Breakdown / Pseudocodes
#### **Enqueue** - adding to the **beginning** of a queue
- This function should accept a value
- Create a new node using the value passed to the fcuntion
- If there are no nodes in the queue, set this node to be the first and last property of the queue
- Otherwise, set the next property on the current last to be that node, and then set the last property of the queue to be that node
- Increment the size of the queue by 1
  ```js
  enqueue(val) {
    const newNode = new Node(val);
    if (!this.first) {
      this.first = newNode;
      this.last = newNode;
    } else {
      this.last.next = newNode;
      this.last = newNode;
    }
    return this.size++;
  }
  ```
#### **Dequeue** - removing from the **beginning** of a queue
- If there is no first property, return null
- Store the first property in a variable
- If there is only 1 node, set the first and last property to be null
- If there is more than 1 node, set the first property to be the next property on the current first
- Decrement the size by 1
- Return the value of the node dequeued
  ```js
  dequeue() {
    if (!this.first) return null;
    let first = this.first;
    if (this.first === this.last) {
      this.last = null;
    }
    this.first = this.first.next;
    this.size--;
    return first.val;
  }
  ```
## Array Implementation
```js
let queue = [];
queue.push("first");
queue.push("second");
queue.push("third");

queue // ["first", "second", "third"]
queue.shift();
// not great because everything gets reindexed
queue // ["second", "third"]
```
```js
// not great because everything gets reindexed
queue.unshift("first");
queue.unshift("second");
queue.unshift("third");

queue // ["third", "second", "first"]
queue.pop();
queue // ["third", "second"]
```