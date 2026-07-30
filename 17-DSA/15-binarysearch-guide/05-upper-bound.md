# Upper Bound

Finds the **first index** where a value strictly greater than the target could be inserted — i.e., the position just past the last occurrence of `target`. Equivalent to C++'s `upper_bound` / Python's `bisect_right`.

## Implementation

```javascript
function upperBound(nums, target) {
  let left = 0;
  let right = nums.length;

  while (left < right) {
    const mid = Math.floor((left + right) / 2);

    if (nums[mid] <= target) {
      left = mid + 1;
    } else {
      right = mid; // nums[mid] > target -> could be the answer, keep searching left
    }
  }

  return left; // first index where nums[index] > target
}

console.log(upperBound([1, 2, 2, 2, 3, 5], 2)); // 4 -> index just past the last 2
console.log(upperBound([1, 2, 2, 2, 3, 5], 4)); // 5 -> would insert before index 5 (value 5)
console.log(upperBound([1, 3, 5], 0)); // 0
console.log(upperBound([1, 3, 5], 6)); // 3
```

## Use case — Last occurrence of a target in a sorted array with duplicates

```javascript
function lastOccurrence(nums, target) {
  const idx = upperBound(nums, target) - 1;
  return idx >= 0 && nums[idx] === target ? idx : -1;
}

console.log(lastOccurrence([1, 2, 2, 2, 3], 2)); // 3
```

## Use case — Count occurrences of a target (paired with Lower Bound)

```javascript
function lowerBound(nums, target) {
  let left = 0,
    right = nums.length;
  while (left < right) {
    const mid = Math.floor((left + right) / 2);
    if (nums[mid] < target) left = mid + 1;
    else right = mid;
  }
  return left;
}

function countOccurrences(nums, target) {
  return upperBound(nums, target) - lowerBound(nums, target);
}

console.log(countOccurrences([1, 2, 2, 2, 3, 5], 2)); // 3
```

## Lower Bound vs Upper Bound, side by side

| Function     | Comparison in loop    | Finds...                            |
| ------------ | --------------------- | ----------------------------------- |
| `lowerBound` | `nums[mid] < target`  | first index with value **≥** target |
| `upperBound` | `nums[mid] <= target` | first index with value **>** target |

The only difference is a single `<` vs `<=` — but it changes whether you land on the first or the position-after-last occurrence.

## Complexity

O(log n) time, O(1) space.

## Where these show up

LeetCode "Find First and Last Position of Element in Sorted Array," counting elements in a range, insertion point problems (`Array.prototype` doesn't have a built-in binary insert, so this pattern fills that gap).
