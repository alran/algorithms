# Quick Find / Quick Union / Union Find

### Purpose
Discover if two elements are part of the same connected component

|algorithm|initialize|union|connected|
|---|---|---|---|
|quick-find|N|N|1|
|quick-union|N|N|N|
|weighted quick-union|N|lgN|lgN|
|path compression quick-union| | | |

## Quick Find

### Summary
Array data structure. Each element is represented by an index
in the array. Two elements are connected if they have the same
value in the array.

### Walkthrough

Start with an empty array.
```
  0 1 2 3 4 5 6 7 8
[ _ _ _ _ _ _ _ _ _ ]
```

Assume that each element points to itself 
(an element alone is its own connected component)
```
  0 1 2 3 4 5 6 7 8
[ 0 1 2 3 4 5 6 7 8 ]
```

To connect one element to another, update the value of the 
element being connected to match the one it is being connected 
to.
```
1 -> 2
  0 1 2 3 4 5 6 7 8
[ 0 2 2 3 4 5 6 7 8 ]
    - -
```

If connecting an element that already has elements connected to
it, make sure to replace that value everywhere with the new connection.

```
2 -> 4
  0 1 2 3 4 5 6 7 8
[ 0 4 4 3 4 5 6 7 8 ]
    - -   -
```

### Pros / Cons
Unioning two elements using this approach is way too expensive (could be N
accesses in a huge array). Trees end up being flat, but its expensive to
keep them this way.

## Quick Union

### Summary
Array data structure. Each element is represented by an index
in the array. The value at each index is the id of the parent.
Two elements are connected if they have the same root. To find
the root, follow the path of parents until the index is the same
as the value.

### Walkthrough

Start with an empty array.
```
  0 1 2 3 4 5 6 7 8
[ _ _ _ _ _ _ _ _ _ ]
```

Assume that each element points to itself 
(an element alone is its own connected component)
```
  0 1 2 3 4 5 6 7 8
[ 0 1 2 3 4 5 6 7 8 ]
```

To connect one element to another, update the value of the 
element being connected to match the root of the one it is 
being connected to.
```
1 -> 2
  0 1 2 3 4 5 6 7 8
[ 0 2 2 3 4 5 6 7 8 ]
    -
```

If connecting an element that already has elements connected to
it, only change the value of the connecting element. Find the root
of the element its being connected to and update its value to match.

```
2 -> 4
  0 1 2 3 4 5 6 7 8
[ 0 2 4 3 4 5 6 7 8 ]
      -   
    
5 -> 2
  0 1 2 3 4 5 6 7 8
[ 0 2 4 3 4 4 6 7 8 ]
            -
```

### Pros / Cons
Find is too expensive - we can make some really tall trees.

## Weighted Quick Union

### Summary
Same as Quick Union, but avoid making tall trees by always
connecting the smaller tree to the root of the larger tree.
Instantiate an extra array that keeps track of length of trees.

### Walkthrough

Start with two empty arrays.
```
  0 1 2 3 4 5 6 7 8
[ _ _ _ _ _ _ _ _ _ ]
```

Assume that each element points to itself (an element alone 
is its own connected component). Assume that all trees prior
to connections start off at size 1.
```
        0 1 2 3 4 5 6 7 8
szs = [ 1 1 1 1 1 1 1 1 1 ]
ids = [ 0 1 2 3 4 5 6 7 8 ]
```

To connect one element to another, update the value of the
smaller tree between the two to match the root of the one it 
is being connected to.
```
1 -> 2
        0 1 2 3 4 5 6 7 8
szs = [ 1 1 2 1 1 1 1 1 1 ]
            -
ids = [ 0 2 2 3 4 5 6 7 8 ]
          - -
```

If connecting an element that already has elements connected to
it, only change the value of the connecting element. Find the root
of the element its being connected to and update its value to match.
Update the sizes array - add the size of the smaller component
to the size of the larger component.

```
2 -> 4
        0 1 2 3 4 5 6 7 8
szs = [ 1 1 3 1 1 1 1 1 1 ]
            -
ids = [ 0 2 2 3 2 5 6 7 8 ]
                -   
    
5 -> 2
        0 1 2 3 4 5 6 7 8
szs = [ 1 1 4 1 1 1 1 1 1 ]
            -
ids = [ 0 2 2 3 2 2 6 7 8 ]
                  -
```

## Weighted Quick Union with Path Compression

### Summary
While computing the root of a number, follow up and make the nodes 
you pass through also point to that root.
