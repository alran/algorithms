# Selection Sort

### Purpose
Sort an array of items

### Summary
Iterate through array and find index of lowest number. switches that number with the
number in the first spot. goes to next char in the array and tries to replace it with
the next smallest.

### Big O
N^2

### Javascript

```javascript
function selectionSort(array) {
  let masterIdx = 0;
  let lowestIdx = 0;

  while (masterIdx < array.length - 1) {
    let helperIdx = masterIdx + 1;

    while (helperIdx <= array.length - 1) {
      const current = array[helperIdx];
      if (current < array[lowestIdx]) {
        lowestIdx = helperIdx;
      }

      if (helperIdx === array.length - 1) {
        const prevLowest = array[masterIdx]
        array[masterIdx] = array[lowestIdx];
        array[lowestIdx] = prevLowest;
      }

      helperIdx++;
    }

    masterIdx++;
    lowestIdx = masterIdx;
  }

  return array;
}
```

