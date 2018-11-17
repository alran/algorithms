# Mergesort

### Purpose
Sort an array of items.

### Summary
Divide the array in half, recursively sort each half, merge the two halves. Cons: 
too much overhead for small arrays

### Big O
N log N

### Javascript

```javascript
function merge(left, right) {
  let ptr1 = 0;
  let ptr2 = 0;
  let final = [];

  while (ptr1 < left.length || ptr2 < right.length) {
    if (!right[ptr2] || (left[ptr1] && left[ptr1] < right[ptr2])) {
      final.push(left[ptr1]);
      ptr1++;
    } else {
      final.push(right[ptr2]);
      ptr2++;
    }
  }

  return final;
}

function mergeSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }

  const middle = Math.floor(length / 2);
  const left = arr.slice(0, middle);
  const right = arr.slice(middle);

  return merge(mergeSort(left), mergeSort(right));
}
```
