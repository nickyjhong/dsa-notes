# Hash Tables
[⬅ Go Back to Home](../README.md)

[⬅ Go Back to Topic](/hash-tables.md)

## Notes
- This is done using a hash function NOT the built-in JavaScript methods

## Big O
- Time:
  - Insert: O(1)
  - Deletion: O(1)
  - Access: O(1)
  
## Code
### Full Code
```js
class HashTable {
  constructor(size=53){
    this.keyMap = new Array(size);
  }
  _hash(key) {
    let total = 0;
    let WEIRD_PRIME = 31;
    for (let i = 0; i < Math.min(key.length, 100); i++) {
      let char = key[i];
      let value = char.charCodeAt(0) - 96
      total = (total * WEIRD_PRIME + value) % this.keyMap.length;
    }
    return total;
  }
  set(key, value) {
    let index = this._hash(key);
    if (!this.keyMap[index]) {
      this.keyMap[index] = []
    }
    this.keyMap[index].push([key, value])
  }
  get(key) {
    let index = this._hash(key);
    if(this.keyMap[index]) {
      for (let i = 0; i < this.keyMap[index].length; i++) {
        if(this.keyMap[index][i][0] === key) {
          return this.keyMap[index][i][1]
        }
      }
    }
    return undefined;
  }
  keys() {
    let keysArr = []
    for (let i = 0; i < this.keyMap.length; i++) {
      if(this.keyMap[i]) {
        for(let j = 0; j < this.keyMap[i].length; j++) {
          if(!keysArr.includes(this.keyMap[i][j][0])) {
            keysArr.push(this.keyMap[i][j][0])
          }
        }
      }
    }
    return keysArr;
  }
  values() {
    let valuesArr = []
    for (let i = 0; i < this.keyMap.length; i++) {
      if(this.keyMap[i]) {
        for(let j = 0; j < this.keyMap[i].length; j++) {
          if(!valuesArr.includes(this.keyMap[i][j][1])) {
            valuesArr.push(this.keyMap[i][j][1])
          }
        }
      }
    }
    return valuesArr;
  }
}
```
### Pseudocodes / Breakdown
#### **Set**
  - Accepts a key and a value
  - Hashes the key
  - Stores the key-value pair in the hash table array via separate chaining
  ```js
  set(key, value) {
    let index = this._hash(key);
    // if there isn't an array there already, make one
    if(!this.keyMap[index]) {
      this.keyMap[index] = []
    }
    this.keyMap[index].push([key, value])
  }
  // EMPTY -> [ , ,[[key, value]] , , ]
  // ALREADY HAS SOMETHING -> [ , ,[[key, value], [key,value]] , , ]
  ```
#### **Get**
  - Accepts a key
  - Hashes the key
  - Retrieves the key-value pair in the hash table
  - If the key isn't found, returns undefined
  ```js
  get(key) {
    let index = this._hash(key);
    if(this.keyMap[index]) {
      for (let i = 0; i < this.keyMap[index].length; i++) {
        if(this.keyMap[index][i][0] === key) {
          return this.keyMap[index][i][1]
        }
      }
    }
    return undefined;
  }
  ```
#### **Keys** - loops through the hash table array and returns an array of keys in the table
```js
keys() {
  let keysArr = []
  for (let i = 0; i < this.keyMap.length; i++) {
    if(this.keyMap[i]) {
      for(let j = 0; j < this.keyMap[i].length; j++) {
        if(!keysArr.includes(this.keyMap[i][j][0])) {
          keysArr.push(this.keyMap[i][j][0])
        }
      }
    }
  }
  return keysArr;
}
```
#### **Values** - loops through the hash table array and returns an array of values in the table
```js
values() {
  let valuesArr = []
  for (let i = 0; i < this.keyMap.length; i++) {
    if(this.keyMap[i]) {
      for(let j = 0; j < this.keyMap[i].length; j++) {
        if(!valuesArr.includes(this.keyMap[i][j][1])) {
          valuesArr.push(this.keyMap[i][j][1])
        }
      }
    }
  }
  return valuesArr;
}
```