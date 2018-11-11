# Prime Numbers

## Checking if a number is prime

The nieve way to check if a number is prime is to iterate from 2 through N-1,
checking for divisibility on each iteration.

An upgrade to this is to only check numbers 2 through the square root of N.

However, we also know that all non-prime numbers are divisible by a prime
number. We can iterate through the prime numbers from 2 through the 
square root of N to discover if a number is prime. (Sieve of 
Eratosthenes)

```javascript
function sieveOfEratosthenes(num) {
  let used = { 0: true, 1: true };
  let count = 0;
  let prime = 2;
  while (prime < Math.sqrt(num)) {
    // cross off remaining multiples of prime
    crossOff(used, prime);
    
    // find next value which is true
    prime = getNextPrime(used, prime);
  }
}

function crossOff(used, prime) {
  // cross off the remaining multiples of prime. Start with prime * prime
  // because if we already have k * prime, where k < prime, this value would
  // have already been crossed off in a prior iteration
  
  for (let i = prime * prime; i < Object.keys(used).length; i += prime) {
    used[i] = true;
  }
}

function getNextPrime(used, prime) {
  let next = prime + 1;
  while (next < Object.keys(used).length && used[next]) {
    next++;
  }
  return next;
}
```
