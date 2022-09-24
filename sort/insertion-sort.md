# Insertion Sort
[⬅ Go Back to Home](../README.md)

[⬅ Go Back to Topic](/sort.md)

## Notes
- Similar to bubble and selection sorts
- Builds up the sort by gradually creating a larger left portion which is always sorted

## Big O
- Time: O(n^2)
- Space: O(1)

## Pseudocode
- Start by picking the second element in the array
- Now compare the second element with the one before it and swap if necessary
- Continue to the next element and if it is in the incorrect order, iterate through the sorted portion (i.e. the left side) to place the element in the correct place
- repeat until the array is sorted

## Code
```js
function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    let current = arr[i]
    for (let j = i - 1; j >= 0 && arr[j] > current; j--) {
      arr[j + 1] = arr[j]
    }
    arr[j + 1] = current
  }
  return arr;
}

insertionSort([2, 1, 9, 76, 4])
```