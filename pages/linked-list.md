# Linked List

### Purpose
Create a linear collection of elements whose order is not based on physical
location in memory

### Summary
Nodes have knowledge of the next item in the list (and the previous, if its
a doubly linked list). The Linked List points to the first node and includes
other helpful functions for adding or removing nodes at the right location.

### Javascript

```javascript
function Node(value, next, prev) {
  this.value = value;
  this.next = next;
  this.prev = prev;
}

class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  addToHead(value) {
    const newNode = new Node(value, this.head, null);
    if (this.head) {
      this.head.prev = newNode;
    } else {
      this.tail = newNode;
    }

    this.head = newNode;
  }

  removeHead() {
    if (!this.head) { return; }

    const nextNode = this.head.next;
    this.head = nextNode;

    if (this.head) {
      this.head.prev = null;
    } else {
      this.tail = null;
    }
  }
}

```

### Ruby

```ruby
class Node
  attr_accessor :data, :pointer

  def initialize(data, pointer = nil)
    @data = data
    @pointer = pointer
  end
end
```

### C

```c
typedef struct node
{
  int data;
  struct node* pointer;
}
```
