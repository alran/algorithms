# Shuffle

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

# Pick Randomly

### Purpose

Randomly choose a set of m integers from an array

### Summary

Move the first m elements into another array. Loop through the rest of the
original array starting at index m. Get a random number at each iteration.
If rand is less than m, swap the element into the other array.

```javascript
function pickRandom(arr, m) {
  const final = arr.slice(0, m);
  for (let i = m; i < arr.length; i++) {
    const rand = Math.floor(Math.random() * (i + 1));
    if (rand < m) {
      final[rand] = arr[i];
    }
  }

  return final;
}
```

