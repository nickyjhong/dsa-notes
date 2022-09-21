# Types of Sorts
[⬅ Go Back](/sort.md)

## Why do I need to know different types of sorts?
- There are many different ways to sort things, and different techniques have their own advantages and disadvantages
- Classic interview topic because it has so many different approaches

## Sorts
#### JavaScript built-in sort method
- But it doesn't always work the way you expect
  ```js
  [6, 4, 15, 10].sort();
  // [10, 15, 4, 6]
  ```
- Accepts an optional *comparator* function to say how to sort

### Less commonly used sort methods because they're less efficient:
#### [Bubble Sort](/sort/bubble-sort.md) - Largest value "bubbles" up to the top
- Time: O(n^2)
#### [Selection Sort](/sort/selection-sort.md) - Smallest value is placed at the beginning on each pass
- Time: O(n^2)
#### [Insertion Sort](/sort/insertion-sort.md) - Build up a sort on left portion of array by inserting/swapping values
- Time: O(n^2)

### More advanced sort methods:
#### [Merge Sort](/sort/merge-sort.md)

#### [Quick Sort](/sort/quick-sort.md)

#### [Radix Sort](/sort/radix-sort.md)
