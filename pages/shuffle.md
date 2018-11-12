# Shuffling

### Purpose

Randomize the order of elements in an array

### Summary

Loop through every element in the array. In each iteration,
find a random integer between 0 and i. Swap array[i] and 
array[rand].

### Complexity

Linear time! O(N)

```javascript
function kuthShuffle(items) {
  const length = items.length;
  for (let i = 0; i < length; i++) {
    const rand = Math.floor(Math.random() * (i + 1));
    const temp = items[rand];
    items[rand] = items[i];
    items[i] = temp;
  }
  return items;
}

```
