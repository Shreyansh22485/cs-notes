# Modular nCr using Fermat's Little Theorem

## Modular Arithmetic:

In modular arithmetic, we work with remainders when integers are divided by a fixed number, called the modulus. The expression 'a mod m' represents the remainder when a is divided by m.

Key properties of modular arithmetic:


```cpp
(a + b) mod m = (a mod m + b mod m) mod m
(a - b) mod m = (a mod m - b mod m + m) mod m
(a * b) mod m = (a mod m * b mod m) mod m
(a / b) mod m = (a mod m * b^(-1) mod m) mod m
```

**NOTE**: Why 10^9+7 is used as modulus?

- It is a large prime number.So we can calculate modular inverse for every number from 1 to $10^9+6$.
- It is within the range of 32-bit integer
- It is a common choice for competitive programming problems
- It helps to avoid overflow and underflow


## Modular Inverse:

In modular arithmetic, the modular inverse of an integer 'a' with respect to a modulus 'm' is an integer 'x' such that:

```cpp
(a * x) mod m = 1
```

The modular inverse exists if and only if 'a' and 'm' are coprime (i.e., their greatest common divisor is 1).

- We use modular inverse to calculate modular division.


## nCr formula:

$$
nCr = \frac{n!}{r! * (n-r)!}
$$

## Modular nCr:

$$
nCr \mod m = \left( \frac{n!}{r! * (n-r)!} \right) \mod m$$

## Fermat's Little Theorem:

Modular inverse using Fermat's Little Theorem:

If m is a prime number, then the modular inverse of a with respect to m is given by:

$$(a^{m-2}) \mod m$$

- We can use binary exponentiation to calculate  $(a^{m-2})\mod m$  in $O(\log m)$  time. 

## Algorithm:

$$
nCr = \frac{n!}{r! * (n-r)!}
$$

Let a = numerator = n!
Let b = denominator = r! * (n-r)!

$$nCr = \frac{a}{b} = (a * b^{-1}) \mod m$$

where $b^{-1}$ is the modular inverse of b with respect to m.

$$(a * b^{-1}) \mod m = (a * (b^{m-2}) \mod m) \mod m$$

$$nCr \mod m = (n! * (r! * (n-r)!)^{m-2}) \mod m$$

## C++ Implementation:

```cpp
const int M = 1e9 + 7;
long long modularnCr(int n, int r){
    if(r < 0 || r > n){
        return 0;
    }
    long long a = fact[n];
    long long b = (fact[r] * fact[n-r])%M;
    
    return a * findPower(b,M-2)%M;
}
```


