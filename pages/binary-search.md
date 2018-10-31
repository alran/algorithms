# Binary Search

### Purpose
finding an element in a sorted array

### Summary
Repeatedly divide the array in half, looking at the lower half if the element
is lower than the dividing number or the upper half if its higher.

### Big O
O(log n)

### Javascript

```javascript
function binarySearch(nums, target) {
  let left = 0;
  let right = nums.length - 1;

  while (left <= right) {
    const middle = left + Math.floor((right - left) / 2);

    if (nums[middle] === target) {
      return middle;
    } else if (nums[middle] < target {
      left = middle + 1;
    } else {
      right = middle - 1;
    }
  }

  return -1;
}
```
