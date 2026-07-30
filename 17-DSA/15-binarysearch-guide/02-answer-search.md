# Answer Search ("Binary Search on the Answer")

Instead of searching for a value's position in an array, you binary search over a **range of possible answers**, using a feasibility check (`canAchieve(x)`) to decide which half to keep. Works whenever the feasibility function is monotonic (once true, stays true — or once false, stays false — as the answer increases).

## Template

```javascript
function binarySearchOnAnswer(low, high, canAchieve) {
  let result = -1;

  while (low <= high) {
    const mid = Math.floor((low + high) / 2);

    if (canAchieve(mid)) {
      result = mid; // mid works — but maybe a smaller/larger value also works
      high = mid - 1; // or `low = mid + 1`, depending on which direction you're optimizing
    } else {
      low = mid + 1; // or `high = mid - 1`
    }
  }

  return result;
}
```

## Example — Koko Eating Bananas

Find the minimum eating speed `k` so Koko finishes all banana piles within `h` hours.

```javascript
function minEatingSpeed(piles, h) {
  let low = 1;
  let high = Math.max(...piles);

  function hoursNeeded(speed) {
    return piles.reduce((total, pile) => total + Math.ceil(pile / speed), 0);
  }

  while (low < high) {
    const mid = Math.floor((low + high) / 2);

    if (hoursNeeded(mid) <= h) {
      high = mid; // mid works — try a slower (smaller) speed
    } else {
      low = mid + 1; // too slow — need to eat faster
    }
  }

  return low;
}

console.log(minEatingSpeed([3, 6, 7, 11], 8)); // 4
```

## Example — Capacity to Ship Packages Within D Days

```javascript
function shipWithinDays(weights, days) {
  let low = Math.max(...weights); // minimum possible: must fit the heaviest package
  let high = weights.reduce((a, b) => a + b, 0); // maximum possible: ship everything in one day

  function daysNeeded(capacity) {
    let days = 1,
      currentLoad = 0;
    for (const w of weights) {
      if (currentLoad + w > capacity) {
        days++;
        currentLoad = 0;
      }
      currentLoad += w;
    }
    return days;
  }

  while (low < high) {
    const mid = Math.floor((low + high) / 2);

    if (daysNeeded(mid) <= days) {
      high = mid; // capacity works — try smaller
    } else {
      low = mid + 1; // need more capacity
    }
  }

  return low;
}
```

## The mental shift

Instead of asking "is the target at this index?", you ask "**is this candidate answer good enough?**" — and binary search over the space of possible answers (which can be values, speeds, capacities, distances) rather than array indices.

## Complexity

O(log(range) × cost of feasibility check) — e.g. O(log(max) × n) for the examples above.

## Recognize this pattern when...

The problem asks for a "minimum/maximum X such that condition Y holds" and you can write a function that checks "does X satisfy Y?" in a monotonic way.
