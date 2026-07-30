# Lower Bound

Finds the **first index** where a value greater than or equal to the target could be inserted — i.e., the leftmost position at which `target` would fit without breaking sort order. Equivalent to C++'s `lower_bound` / Python's `bisect_left`.

## Implementation

```javascript
function lowerBound(nums, target) {
  let left = 0;
  let right = nums.length; // note: right starts at length, not length - 1

  while (left < right) {
    const mid = Math.floor((left + right) / 2);

    if (nums[mid] < target) {
      left = mid + 1;
    } else {
      right = mid; // nums[mid] >= target -> could be the answer, keep searching left
    }
  }

  return left; // first index where nums[index] >= target
}

console.log(lowerBound([1, 2, 2, 2, 3, 5], 2)); // 1 -> first index of value 2
console.log(lowerBound([1, 2, 2, 2, 3, 5], 4)); // 5 -> would insert before index 5 (value 5)
console.log(lowerBound([1, 3, 5], 0)); // 0 -> smaller than everything, insert at start
console.log(lowerBound([1, 3, 5], 6)); // 3 -> larger than everything, insert at end
```

## Use case — First occurrence of a target in a sorted array with duplicates

```javascript
function firstOccurrence(nums, target) {
  const idx = lowerBound(nums, target);
  return idx < nums.length && nums[idx] === target ? idx : -1;
}

console.log(firstOccurrence([1, 2, 2, 2, 3], 2)); // 1
```

## Use case — Count occurrences of a target (paired with Upper Bound)

```javascript
function countOccurrences(nums, target) {
  return upperBound(nums, target) - lowerBound(nums, target);
}
// see 05-upper-bound.md for upperBound implementation
```

## Complexity

O(log n) time, O(1) space.

## The core idea

`lowerBound` answers: "**where does the first value ≥ target belong?**" It works even if `target` isn't in the array at all — it just tells you where it _would_ go.
