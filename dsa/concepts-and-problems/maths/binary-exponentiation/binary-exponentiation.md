# Binary Exponentiation or Fast Exponentiation

Binary exponentiation is an efficient algorithm to compute the power of a number. It calculates \(a^b\) in **O(log b)** time complexity, which is much faster than the naive approach of multiplying \(a\) by itself \(b\) times giving a time complexity of O(b).

## Key Concept:

    a^b = (a^(b/2))^2 if b is even

        = a * (a^((b-1)/2))^2 if b is odd

## C++ Implementation:

```cpp
#include <bits/stdc++.h>
using namespace std;

// Recursive function to calculate a^b
long long findPower(long long a, long long b) {
    if (b == 0) {
        return 1; // Base case: a^0 = 1
    }
    long long half = findPower(a, b / 2);
    long long result = half * half;
    if (b % 2 == 1) {
        result *= a;
    }
    return result;
}

// Iterative function to calculate a^b
long long findPower(long long a, long long b) {
    long long result = 1;
    while (b > 0) {
        if (b % 2 == 1) {
            result *= a; // If b is odd, multiply the result by a
        }
        a *= a; // Square the base
        b /= 2; // Halve the exponent
    }
    return result;
}
```
- Time Complexity: O(log b) to the base of 2 due to the recursive halving of the exponent
- Space Complexity: O(log b) due to recursion stack

