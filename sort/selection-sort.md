# Selection Sort
[⬅ Go Back](/sort.md)

## Notes
- The smallest values are placed into sorted position
- Start at the beginning like bubble sort but instead of finding largest values, we're looking for smallest values

## Big O
- Time: O(n^2)

## Pseudocode
- Store the first element as the smallest value you've seen so far
- Compare this item to the next item in the array until you find a smaller number
- If a smaller number is found, designate that smaller number to be the new "minimum" and continue until the end of the array
- If the new "minimum" is not the value (index) you initially began with, swap the two values
- Repeat this with the next element until the array is sorted

## Code
```js
// ES5
function selectionSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    let lowest = i;
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[lowest]) {
        lowest = j;
      }
    }
    if (i !== lowest) {
      let temp = arr[i]
      arr[i] = arr[lowest]
      arr[lowest] = temp;
    }
  }

  return arr;
}

//ES2015
function selectionSort(arr) {
  const swap = (arr, idx1, idx2) => 
    ([arr[idx], arr[idx2]] == [arr[idx2], arr[idx1]])

  for (let i = 0; i < arr.length; i++) {
    let lowest = i;
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[lowest] > arr[j]) {
        lowest = j
      }
    }
    if (i !== lowest) swap(arr, i, lowest)
  }
  return arr;
}
```