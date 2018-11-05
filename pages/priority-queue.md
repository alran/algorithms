# Priority Queue

### Purpose
Store items based on a given priority. When grabbing something
from the queue, the highest priority item comes off first.

### Summary
Doubly linked list with priority value stored on each node.
On insertion, the node is placed between a higher and lower
node. On removal, the head is removed and the node after the
head takes its place.

### Javascript

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
