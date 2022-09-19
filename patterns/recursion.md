# Reursion
[⬅ Go Back](/patterns.md)

<p align="center">
  <img src="images/recursion.jpg" alt="drawing" width=500px />
</p>

## What is recursion?!
- Taking a problem and doing it over and over in smaller pieces
  - A process (a function) that calls itself

## Call Stack
- A **stack** data structure
- When a function is invoked, it is placed (pushed) on top of the call stack
- When JavaScript sees the return keyword, the function ends and the compiler will remove (pop) the function from the call stack
- Need a base case or call stack will go on forever!

## Essential parts of a recursive function
### Base case
- The condition when the recursion ends (like how a while loop needs a condition to stop) / stopping point

### Recursive call that shrinks
- Input that gets modified until the base case is called


## Examples
### sumRange
```js
function sumRange(num) {
  if (num === 1) return 1;
  return num + sumRange(num - 1)
}

// How it works:

sumRange(3)
  return 3 + sumRange + (2)
                return 2 + sumRange(1)
                              return 1

sumRange(3)
  return 3 + 3
```

### factorial
```js
// For-loop
function factorial(num) {
  let total = 1;
  for (let i = num; i > 0; i--) {
    total *= i
  }
  return total;
}

// Recursion
function factorial(num) {
  if (num === 1) return 1;
  return num * factorial(num - 1)
}
```
### collectOddValues
#### Helper method recursion
```js
function collectOddValues(arr) {
  // if we put result inside helper, the array would be reset every single time the helper is run
  let result = []

  function helper (helperInput) {
    if (helperInput.length === 0) {
      return;
    }
    if (helperInput[0] % 2 !== 0) {
      result.push(helperInput[0])
    }
    helper(helperInput.slice(1))
  }
  helper(arr)
  return result;
}
```

#### Pure recursion
```js
function collectOddValues(arr) {
  let newArr = []
  if (arr.length === 0) {
    return newArr;
  }
  if (arr[0] % 2 !== 0) {
    newArr.push(arr[0])
  }
  newArr = newArr.concat(collectOddValues(arr.slice(1)))
  return newArr;
}

// newArr explanation
collectOddValues([1, 2, 3, 4, 5])
[1].concat(collectOddValues([2, 3, 4, 5]))
            [].concat(collectOddValues([3, 4, 5]))
                      [3].concat(collectOddValues([4, 5]))
                                  [].concat(collectOddValues([4, 5]))
                                              [5].concat(collectOddValues([4, 5]))
                                                          [].concat(collectOddValues([]))

[5].concat([]) = [5]
[0].concat([5]) = [5]
[3].concat([5]) = [3, 5]
[0].concat([3, 5]) = [3, 5]
[1].concat([3, 5]) = [1, 3, 5]
```
Tips for pure recusion:
- For arrays, use methods like **slice**, **the spread operator**, and **concat** that make copies of arrays so you do not mutate them
- Remember that strings are immutable so you need to use methods like **slice**, **substr**, or **substring** to make copies of strings
- Make copies of objects using **Object.assign**, or **the spread operator**