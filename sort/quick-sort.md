# Quick Sort
[⬅ Go Back](/sort.md)

## Notes
- Like merge sort, it exploits the fact that arrays of 0 or 1 element are always sorted
- Worked by selecting one element (called the "pivot") and finding the index where the pivot should end up in the sorted array
- Once the pivot is positioned appropriately, quick sort can be applied on either side of the pivot

## Big O
- Time:
  - Best and average: O(n log n)
  - Worst: O(n^2)
- Space: O(log n)

## Pivot
- In order to implement quick sort, it's useful to first implement a function responsible for arranging elements in an array on either side of a pivot
- Given an array, this helper function should designate an element as the pivot
- It should then rearrange elements in the array so that all values less than the pivot are moved to the left of the pivot, and all values greater than the pivot are moved to the right of the pivot
- The order of elements on either side of the pivot doesn't matter
- The helper should do this **in place**, that is, it should not create a new array
- When complete, the helper should return the index of the pivot
### Picking a pivot
- The runtime of quick sort depends in part on how the pivot is selected
- Ideally, the pivot should be chosen so that it's roughly the median value in the data set you're sorting
- For simplicity, we'll always choose the pivot to be the first element (there are consequences to this)
### Example
```js
let arr = [5, 2, 1, 8, 4, 7, 6, 3]
pivot(arr) // 4 -> this is the INDEX

arr;
// any one of these is an acceptable mutation / there are others :
// [2, 1, 4, 3, 5, 8, 7, 6]
// [1, 4, 3, 2, 5, 7, 6, 8]
// [3, 2, 1, 4, 5, 7, 6, 8]
// [4, 1, 2, 3, 5, 6, 8, 7]

// In the final sorted array, the 4th index is in its final position
```
### Pseudocode
- It will help to accept three arguments: an array, a start index, and an end index (these can default to 0 and the array length minus 1, respectively)
- Grab the pivot from the start of the array
- Store the current pivot index in a variable (this will keep track of where the pivot should end up)
- Loop through the array from the start until the end
  - If the pivot is greater than the current element, increment the pivot index variable and then swap the current element with the element at the pivot index
- Swap the starting element (i.e., the pivot) with the pivot index
- Return the pivot index
### Code
```js
// ES5
function pivot(arr, start = 0, end = arr.length-1) {
  // basic swap function that takes an array and two indices to swap
  function swap(arr, i, j) {
    let temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp 
  }

  let pivot = arr[start]
  let swapIdx = start; // starts at 0

  for (let i = start + 1; i < arr.length; i++) {
    if (pivot > arr[i]) {
      swapIdx++; // something is greater than value of index 0
      swap(arr, swapIdx, i)
    }
  }
  swap(arr, start, swapIdx) // swap start and swapIdx not pivot
  return swapIdx
}

pivot([4, 8, 2, 1, 5, 7, 6, 3]) // 3
// [4, 8, 2, 1, 5, 7, 6, 3]
// [4, 2, 8, 1, 5, 7, 6, 3]
// [4, 2, 1, 8, 5, 7, 6, 3]
// [4, 2, 1, 3, 5, 7, 6, 8]

// take swap index and swap with the start so that 4 is in the correct position
// [3, 2, 1, 4, 5, 7, 6, 8]

// ES2015
function pivot(arr, start = 0, end = arr.length - 1) {
  const swap = (arr, idx1, idx2) => {
    [arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]]
  }

  let pivot = arr[start]
  let swapIdx = start

  for (let i = start + 1; i <= end; i++) {
    if (pivot > arr[i]) {
      swapIdx++
      swap(arr, swapIdx, i)
    }
  }
  swap(arr, start, swapIdx)
  return swapIdx
}
```
## Sorting
### Pseudocode
- Call the pivot helper on the array the beginning
- When the helper returns the updated pivot index, recursively call the pivot helper on the subarray to the left of that index, and the subarray to the right of that index
- Base case occurs when you consider a subarray with less than 2 elements
### Code
```js
function quickSort(arr, left = 0, right = arr.length - 1) {
  if (left < right ) {
    let pivotIdx = pivot(arr, left, right) // 3
    // left
    quickSort(arr, left, pivotIdx - 1)
    // right
    quickSort(arr, pivotIdx + 1, right);
  }
  return arr;
}

quickSort([4, 6, 9, 1, 2, 5, 3])
// [4, 6, 9, 1, 2, 5, 3]
// [3, 2, 1, 4, 6, 9, 5] -> pivot figures out that 4 needs to be at index 3
//           4
//  3, 2, 1     6, 9, 5
//        3       6
//  2, 1        5     9
//     2
//  1
```