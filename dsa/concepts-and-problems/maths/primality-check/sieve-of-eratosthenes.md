# Sieve of Eratosthenes

The Sieve of Eratosthenes is an efficient algorithm for finding all prime numbers up to a specified integer. It works by iteratively marking the multiples of each prime number starting from 2.

## How to check if a number is prime or not ?

**Prime number** is a natural number greater than 1 that cannot be formed by multiplying two smaller natural numbers. A prime number is only divisible by 1 and itself.

- 1st Approach: Check for all numbers from 2 to n-1 if they divide n or not. If any number divides n, then it is not prime.
    - Time Complexity: O(n)
```cpp
bool isPrime(int n) {
    if (n <= 1) return false;
    for (int i = 2; i < n; i++) {
        if (n % i == 0) return false;
    }
    return true;
}
```
- 2nd Approach: Check for all numbers from 2 to n/2 if they divide n or not. If any number divides n, then it is not prime.
    - Time Complexity: O(n/2)
```cpp
bool isPrime(int n) {
    if (n <= 1) return false;
    for (int i = 2; i <= n / 2; i++) {
        if (n % i == 0) return false;
    }
    return true;
}
```
- 3rd Approach: Check for all numbers from 2 to sqrt(n) if they divide n or not. If any number divides n, then it is not prime.
    - Time Complexity: O(sqrt(n))
```cpp
bool isPrime(int n) {
    if (n <= 1) return false;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) return false;
    }
    return true;
}
```

## Sieve of Eratosthenes

Find all prime numbers up to a given number n 

### Algorithm:
1. Create a boolean array `isPrime[0..n]` and initialize all entries as true. A value in `isPrime[i]` will be false if i is Not a prime, else true.
2. Set `isPrime[0]` and `isPrime[1]` to false, since 0 and 1 are not prime numbers.
3. For each number p from 2 to sqrt(n):
   - If `isPrime[p]` is true, then mark all multiples of p (i.e., 2p, 3p, 4p, ...) as false in the `isPrime` array.

```cpp
void sieveOfEratosthenes(int n) {
    vector<bool> isPrime(n + 1, true);
    isPrime[0] = isPrime[1] = false; // 0 and 1 are not prime numbers

    for (int i = 2; i * i <= n; i++) {
        if (isPrime[i]) {
            for(int j = 2; j * i <= n; j++) {
                isPrime[j * i] = false; // Mark multiples of i as not prime
            }
        }
    }

    // Print all prime numbers
    for (int i = 2; i <= n; i++) {
        if (isPrime[i]) {
            cout << i << " ";
        }
    }
}
```
#### Time Complexity: **O(n log log n)**

For every i, we are marking n/i numbers as false. 

$$
= n*(1/2 + 1/3 + 1/5 + 1/7 + ... ) 
= O(n log log n)
$$

*Harmonic series of primes grows slower than the harmonic series of all numbers, which is why the time complexity is O(n log log n).*