# Bit Manipulation

## Addition

Addition for binary numbers is set up the same as for 
decimal numbers. However, because binary numbers use 
base 2 instead of base 10, any number over 1.

```
  0110
+ 0010
------
  1000
```
```
1 + 1 = 0 (carry 1)
1 + 1 + 1 = 1 (carry 1)
0 + 0 = 0
0 + 1 = 1
```

Note: if you add a number to itself, it is the equivalent
of multiplying it by 2 (0010). Multiplying a number by 2
is the equivalent of left shifting by 1.

## Subtraction

The main difference with subtraction is that when you
borrow from the number to the left, you borrow two
instead of 10.

```
  0110
- 0011
------
  0011
```
```
1 - 1 = 0
0 - 1 = 1 (borrow 2 from the one to the left)
0 - 0 = 0
```

## XOR (^)

When you XOR a binary number against another number,
you return 1 anytime the bits are different. You
return 0 anytime they are the same.

```
  1101
^ 0101
------
  1000
```
```
1 ^ 0 = 1
0 ^ 0 = 0
1 ^ 1 = 0
```

## OR (|)

Unlike XOR, OR returns 1 if at least one of the 
comparators is 1. Meaning, if both bits are 0,
the result will be 0. Otherwise, the result is 1.

```
1 | 1 = 1
1 | 0 = 1
0 | 0 = 0
```

## AND (&)

When you AND a binary number against another number,
you return 1 anytime both bits are 1. Otherwise the
result is 0.

```
1 & 1 = 1
0 & 1 = 0
0 & 0 = 0
```

## Left Shift (<<)

Move all bits left by the number specified, appending
0's at the end.

```
1111 << 2 = 1100
```

## Right Shift (>>)

Move all bits right by the number specified, prepending
0's at the front.

```
1111 >> 2 = 0011 
```

## Multiplication (*)

Binary multiplication is the same as decimal multiplication.
However, there are some shortcuts. Multiplying by 2 (0010) is
the same as left shifting by 1. Multiplying by 4 (0100) is the
same as left shifting by 2. Multiplying by 8 (1000) is the same
as left shifting by 3.

```
  0011
* 0101
------
  0011
 0000x
0011xx
------
  1111
```

## NOT (~)

This returns the reverse of the number.

```
~0 = 1111
~1101 = 0010
```

## Two's Compliment

Computers typically store integers in a two's compliment
representation. To get there, invert the bits of a positive 
number and add one.

```
-2 -> 110
-1 -> 111
0  -> 000
1  -> 001
2  -> 010
```

## Getting and Setting

### Get Bit

To find a bit based on its index in a binary number,
left shift 1 (0001) by the index and AND the result
with the original number. If this result is 0, the bit
is 0. If the result is anything else, the bit is 1.

```javascript
function getBit(num, idx) {
  return (num & (1 << idx)) !== 0);
}

getBit(1000, 3) // true
getBit(1000, 1) // false
```

### Set Bit

To set a bit at a specific index (make it 1), left 
shift 1 (0001) by the index and OR the result with 
the original number.

```javascript
function setBit(num, idx) {
  return num | (1 << i);
}
```

### Clear Bit

To clear a bit at a specific index, left shift 1 (0001)
by the index and get the opposite of the result (~).
Then, AND the original number with this result. Do
basically the opposite of `setBit`.

```javascript
function clearBit(num, i) {
  const mask = ~(1 << i);
  return num & mask;
}
```

### Update Bit

To set a bit at a specific index to a value that you
specify, clear the bit at the index using `clearBit`,
then OR that result with your value left shifted by
the index.

```javascript
function updateBit(num, i, bitIsOne) {
  const value = bitIsOne ? 1 : 0;
  const mask = ~(1 << i);
  return (num & mask) | (value << i);
}
```

