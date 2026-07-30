# Rotated Array

A sorted array that's been rotated at some unknown pivot (e.g. `[4,5,6,7,0,1,2]`). It's no longer fully sorted, but **at least one half around any midpoint is always sorted** — that property is what makes binary search still applicable.

## Search in Rotated Sorted Array (no duplicates)

```javascript
function searchRotated(nums, target) {
  let left = 0;
  let right = nums.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);

    if (nums[mid] === target) return mid;

    if (nums[left] <= nums[mid]) {
      // left half is sorted
      if (nums[left] <= target && target < nums[mid]) {
        right = mid - 1;
      } else {
        left = mid + 1;
      }
    } else {
      // right half is sorted
      if (nums[mid] < target && target <= nums[right]) {
        left = mid + 1;
      } else {
        right = mid - 1;
      }
    }
  }

  return -1;
}

console.log(searchRotated([4, 5, 6, 7, 0, 1, 2], 0)); // 4
console.log(searchRotated([4, 5, 6, 7, 0, 1, 2], 3)); // -1
```

## Find Minimum in Rotated Sorted Array

```javascript
function findMin(nums) {
  let left = 0;
  let right = nums.length - 1;

  while (left < right) {
    const mid = Math.floor((left + right) / 2);

    if (nums[mid] > nums[right]) {
      // minimum must be to the right of mid (rotation point is ahead)
      left = mid + 1;
    } else {
      // mid could be the minimum, or minimum is to the left
      right = mid;
    }
  }

  return nums[left];
}

console.log(findMin([4, 5, 6, 7, 0, 1, 2])); // 0
```

## The key decision at every step

1. Compare `nums[mid]` to `nums[left]` (or `nums[right]`) to figure out **which half is sorted**.
2. Check whether the target falls within that sorted half's range.
3. If yes, search that half; if no, search the other half.

## Complexity

O(log n) time, O(1) space — same as classic binary search, just with an extra check per step to determine which half is sorted.

## Recognize this pattern when...

The array is described as "sorted then rotated" or "rotated at an unknown pivot," and you need O(log n) search or minimum-finding.
