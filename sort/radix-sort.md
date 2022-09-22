# Radix Sort
[⬅ Go Back](/sort.md)

## Notes
- Does not make comparisons between elements
- Works on lists of numbers (usually binary numbers)
- Exploits the fact that information about the size of a number is encoded in the number of digits
  - More digits means a bigger number
- Compare using the digit on the right of the number
- The number of times the array is split depends on the number of digits in the largest number

## Big O
- Time: O(nk) -> n is number of things that are being sorted, k is length of the thing being sorted
- Space: O(n + k)

## Helper Functions
### getDigit(num, place) - returns the digit in *num* at the given *place* value
- Think of place values from elementary school - it starts on the RIGHT side!!!
#### Example
```js
getDigit(12345, 0) // 5
getDigit(12345, 1) // 4
getDigit(12345, 2) // 3
getDigit(12345, 3) // 2
getDigit(12345, 4) // 1
getDigit(12345, 5) // 0
```
#### Code
```js
function getDigit(num, place) {
  return Math.floor(Math.abs(num) / Math.pow(10, place)) % 10
}

getDigit(7323, 2)
// 7323 / 100 = 73.23
// Math.floor(73.23) = 73
// 73 % 10 = 3
```
### digitCount(num) - returns the number of digits in num
#### Example
```js
digitCount(1) // 1
digitCount(25) // 2
digitCount(314) // 3
```
#### Code
```js
function digitCount(num) {
  if (num === 0) return 1;
  return Math.floor(Math.log10(Math.abs(num))) + 1;
}

digitCount(423)
// Math.log10(423) = 2.6263403673750423
// Math.floor(2.6263403673750423) = 2
// 2 + 1 = 3

digitCount(21388)
// Math.log10(21388) = 4.330170175428303
// Math.floor(4.330170175428303) = 4
// 4 + 1 = 5
```
### mostDigits(num) - given an array of numbers, returns the number of digits in the largest numbers in the list
- Use digitCount on each number of the list
#### Example
```js
mostDigits([1234, 56, 7]) // 4
mostDigits([1, 1, 11111, 1]) // 5
mostDigits([12, 34, 56, 78]) // 2
```
#### Code
```js
function mostDigits(nums) {
  let maxDigits = 0;
  for (let i = 0; i < nums.length; i++) {
    maxDigits = Math.max(maxDigits, digitCount(nums[i]))
  }
  return maxDigits
}

mostDigits([23, 567, 89, 12234324, 90]) // 8
// mostDigits = 2 (@ 23)
// mostDigits = 3 (@ 567, 89)
// mostDigits = 8 (@ 12234324, 90)
```

## Sort
### Pseudocode
- Define a function that accepts a list of numbers
- Figure out how many digits the largest number has (mostDigits)
- Loop from k = 0 up to this largest numbers of digits
  - For each iteration of the loop:
    - Create buckets (arrays) for each digit (0 to 9)
    - Place each number in the corresponding bucket based on its k-th digit
- Replace our existing array with values in our buckets, starting with 0 and going up to 9
- Return list at the end
### Code
```js
function radixSort(nums) {
  let maxDigitCount = mostDigits(nums)
  for (let k = 0; k < maxDigitCount; k++) {
    let digitBuckets = Array.from({length: 10}, () => []) // creates an array with 10 subarrays
    for (let i = 0; i < nums.length; i++) {
      let digit = getDigit(nums[i], k)
      digitBuckets[digit].push(nums[i])
    }
    nums = [].concat(...digitBuckets) // make new array with numbers in buckets in order to keep sorting
  }
  return nums
}

radixSort([23, 345, 5467, 12, 2345, 9852]) // [12, 23, 345, 2345, 5467, 9852]
// [12, 9852, 23, 345, 2345, 5467] // sorted by last digit (ones place)
// radixSort([12, 9852, 23, 345, 2345, 5467])
// [12, 23, 345, 2345, 9852, 5467] // sorted by second to last digit (tens place)
// radixSort([12, 23, 345, 2345, 9852, 5467])
// [12, 23, 345, 2345, 5467, 9852] // sorted by third to last digit (hundred place)
// radixSort([12, 23, 345, 2345, 5467, 9852])
// [12, 23, 345, 2345, 5467, 9852] // sorted by fourth to last digit (thousands place)
```