# Big O Time in Objects and Arrays
[⬅ Go Back](/big-o.md)

## Objects
- Don't need order
- Use when you need fast access / insertion and removal
- Time in Big O
  - Insertion - O(1)
  - Removal - O(1)
  - Searching - O(n)
  - Access - O(1)
  - Object.keys - O(n)
  - Object.values - O(n)
  - Object.entries - O(n)
  - Object.hasOwnProperty - O(1)

## Arrays
- Ordered lists
- Time in Big O
  - Insertion - depends...
    - .unshift - O(n) 
    - .push - O(1)
  - Removal - depends...
    - .shift - O(n)
    - .pop - O(1)
  - Searching - O(n)
  - Access - O(1)
  - .concat - O(n)
  - .slice - O(n)
  - .splice - O(n)
  - .sort - O(n log n)
  - .forEach/map/filter/reduce/etc - O(n)