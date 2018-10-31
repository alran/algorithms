# Bubble Sort

### Purpose
Sort an array of elements

### Summary
Compare first item with second. if the first item is bigger, switch the two. Continue
doing this until you reach the end of the array or find a larger item (bubbling the
larger number to the end of the array). Continue iterating through the array. Sorts
in place.

### Big O
N^2

### Javascript

```javascript
function bubbleSort(array) {
  const length = array.length;
  let lastIdx = length - 1;

  while (lastIdx >= 0) {
    let leftIdx = 1;

    while (leftIdx <= lastIdx) {
      const prev = array[leftIdx - 1];
      const current = array[leftIdx];

      if (prev && prev > current) {
        array[leftIdx - 1] = current;
        array[leftIdx] = prev;
      }

      leftIdx++;
    }

    lastIdx--;
  }

  return array;
}
```
