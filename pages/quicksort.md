# Quicksort

### Purpose
Sort an array of items

### Summary
Shuffle the array

Partition so that for some j
- entry array[j] is in place
- no larger entry is to the left of j
- no smaller entry is to the right of j

Sort each piece recursively

### Big O
N log N

### Javascript

```javascript
function swap(items, idx1, idx2) {
  const savedVal = items[idx2];
  items[idx2] = items[idx1];
  items[idx1] = savedVal;
}

function partition(items, pivot, left, right) {
  const pivotValue = items[pivot];
  let partitionIdx = left;

  let helperIdx = left;
  while (helperIdx < right) {
    if (items[helperIdx] < pivotValue) {
      swap(items, helperIdx, partitionIdx);
      partitionIdx++;
    }

    helperIdx++;
  }

  swap(items, right, partitionIdx);
  return partitionIdx;
}

function quickSort(items, left = 0, right = items.length -1){
  const length = items.length;
  let pivot;
  let partitionIndex;

  if(left < right){
    pivot = right;
    partitionIndex = partition(items, pivot, left, right);
    quickSort(items, left, partitionIndex - 1); // sort left
    quickSort(items, partitionIndex + 1, right); // sort right
  }

  return items;
}

```
