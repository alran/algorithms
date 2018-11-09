# Trees

## 2-3 Trees

### Purpose
Keep data sorted and allow for quick search

### Summary
Allow 1 or 2 keys per node. With one key, the node has
two children. With two keys, the node has three children.
The left node is less, the middle node is between the keys,
and the right node is greater.

### Pros / Cons
The tree has perfect balance. Every path from root to null
link has the same length. It also has symmetric order. 
In order traversal yields keys in ascending order.

### Complexity
Every operation is guaranteed to be a constant times lg N
(search, insert, delete)

### Walkthrough
To insert a node, walk through the tree until you find
the place the node belongs. If the node it should connect
to has only one key, add the value to that node, making it
a two key node. If the node it is supposed to has two keys
already, create a temporary 3-key node, then split the keys
out into three, passing the middle key to the parent.

## Red-Black BSTs (left-leaning)

### Summary
Represent a 2-3 tree as a BST. Split 3 nodes into binary
search trees with links that lean left.
