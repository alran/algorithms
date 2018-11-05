# Priority Queue

### Purpose
Store items based on a given priority. When grabbing something
from the queue, the highest priority item comes off first.

### Summary
Priority Queues can be implemented in many ways, including
via an unordered array, an ordered array, and a binary
heap.

### Ordered Array
Doubly linked list with priority value stored on each node.
On insertion, the node is placed between a higher and lower
node. On removal, the head is removed and the node after the
head takes its place.

```javascript
function Node(value = null, priority = null) {
  this.value = value;
  this.priority = priority;
  this.next = null;
}

class priorityQueue {
  constructor() {
    this.head = null;
  }

  insert(value, priority) {
    const newNode = new Node(value, priority);
    if (!this.head || priority > this.head.priority) {
      newNode.next = this.head;
      this.head = newNode;
    } else {
      let pointer = this.head;
      while (pointer.next && priority < pointer.next.priority) {
        pointer = pointer.next;
      }
      newNode.next = pointer.next;
      pointer.next = newNode;
    }
  }

  remove() {
    const head = this.head;
    this.head = this.head.next;
    return head;
  }
}
```

### Binary Heap
An array representation of a binary heap, where the first element
is at index 1. The parents of a node k are at k / 2. The children
are at 2k and 2k + 1. To insert an element, add it to the bottom
most element. If it is larger than its parent, switch it with its
parent. If as a parent it is for some reason smaller than one of
its children, switch it with the largest smaller child.

```javascript
class MaxPriorityQueue {
  constructor() {
    this.priorityQueue = [null];
  }

  insert(v) {
    this.priorityQueue.push(v);
    this.swim(this.length() - 1);
    return this.priorityQueue;
  }

  deleteMax() {
    const max = this.priorityQueue[1];
    this.swap(1, this.length() - 1);
    this.sink(1);
    this.priorityQueue[this.length() - 1] = null;
    return max;
  }

  swim(k) {
    while(k > 1 && this.less(k / 2, k)) {
      this.swap(k, k / 2);
      k = k / 2;
    }
  }

  length() {
    return this.priorityQueue.length;
  }

  sink(k) {
    while (2 * k < this.length()) {
      let j = 2 * k;
      if (j < this.length() && this.less(j, j+1)) {
        j++;
      }

      if (!this.less(k, j)) {
        break;
      }

      this.swap(k, j);
      k = j;
    }
  }

  less(i, j) {
    return this.priorityQueue[i] < this.priorityQueue[j];
  }

  swap(i, j) {
    const temp = this.priorityQueue[i];
    this.priorityQueue[i] = this.priorityQueue[j];
    this.priorityQueue[j] = temp;
  }

  isEmpty() {
    return this.priorityQueue.length === 0;
  }
}
```
