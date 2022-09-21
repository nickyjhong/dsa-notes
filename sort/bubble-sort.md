# Bubble Sort
[⬅ Go Back](/sort.md)

## Notes
- **Obama said it's not good to use**
- Not efficient or commonly used
- A sorting algorithm where the largest values "bubble" up to the top
- Before we sort, we must swap
  ```js
  // ES5
  function swap(arr, idx1, idx2) {
    let temp = arr[idx1]
    arr[idx1] = arr[idx2]
    arr[idx2] = temp
  }

  // ES2015
  const swap = (arr, idx1, idx2) => {
    [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]]
  }
  ```

## Big O
- Time: O(n^2)
- Space: O(1)

## Pseudocode
- Start looping with a variable called i from the end of the array towards the beginning
- Start an inner loop with a variable called j from the beginning until i - 1
- If arr[j] is greater than arr[j+1], swap those two values
- Return the sorted array

## Code
```js
function bubbleSort(arr) {
  // OPTIMIZATION
  let noSwaps
  //
  for (let i = arr.length; i > 0; i --) {
    noSwaps = true;
    for (let j = 0; j < i - 1; j++) {
      if (arr[j] > arr[j+1]) {
        let temp = arr[j]
        arr[j] = arr[j + 1]
        arr[j + 1] = temp
        noSwaps = false;
      }
    }
    if (noSwaps) break;
  }
  return arr;
}
```