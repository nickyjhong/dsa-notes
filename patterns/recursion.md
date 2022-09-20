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
// Write a function called recursiveRange which accepts a number and adds up all the numbers from 0 to the number passed to the function 
function sumRange(num) {
  if (num === 0) return 0;
  return num + sumRange(num - 1)
}

// How it works:

sumRange(3)
  return 3 + sumRange + (2)
                return 2 + sumRange(1)
                              return 1 + sumRange(0)
                                            return 0;

sumRange(3)
1 + 0 = 1
2 + 1 = 3
3 + 3 = 6
```

### factorial
```js
// Write a function factorial which accepts a number and returns the factorial of that number. A factorial is the product of an integer and all the integers below it; e.g., factorial four ( 4! ) is equal to 24, because 4 * 3 * 2 * 1 equals 24.  factorial zero (0!) is always 1.

// For-loop
function factorial(num) {
  let total = 1;
  for (let i = num; i >= 0; i--) {
    total *= i
  }
  return total;
}

// Recursion
function factorial(num) {
  if (num === 0) return 1;
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

### power
```js
// Write a function called power which accepts a base and an exponent. The function should return the power of the base to the exponent. This function should mimic the functionality of Math.pow()  - do not worry about negative bases and exponents.

function power (base, exponent) {
  if (exponent === 0) return 1;
  return base * power(base, exponent - 1)
}
```

### productOfArray
```js
// Write a function called productOfArray which takes in an array of numbers and returns the product of them all.

function productOfArray(arr) {
  if (arr.length === 0) return 1;
  return arr[0] * productOfArray(arr.slice(1))
}
```

### fib
```js
// Write a recursive function called fib which accepts a number and returns the nth number in the Fibonacci sequence. Recall that the Fibonacci sequence is the sequence of whole numbers 1, 1, 2, 3, 5, 8, ... which starts with 1 and 1, and where every number thereafter is equal to the sum of the previous two numbers.

function fib(num){
  if (num <= 2) return 1;
  return fib(num-1) + fib(num-2);
}
```

### reverse
```js

```

### isPalindrome
```js

```

### someRecursive
```js

```

### flatten
```js

```

### capitalizeFirst
```js

```

### nestedEvenSum
```js

```

### capitalizeWords
```js

```

### stringifyNumbers
```js

```

### collectStrings
```js

```