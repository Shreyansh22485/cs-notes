# Prefix Sum

## 1D Prefix Sum

$$prefixSum[i] = sum(arr[0...i])$$

**Example**:

```
Input: arr = [1, 2, 3, 4, 5]

Output: prefixSum = [1, 3, 6, 10, 15]
```

### Range Sum

Range sum of arr[L...R] can be calculated as:

$$rangeSum[L...R] = prefixSum[R] - prefixSum[L-1]$$

**Cpp Implementation:**

```cpp
const int N = 1e5 + 7;
int prefixSum[N]; // 1-based indexing

void calculatePrefixSum(int arr[], int n){
    prefixSum[0] = 0; // For 1-based indexing

    for(int i = 1; i <= n; i++){
        prefixSum[i] = prefixSum[i-1] + arr[i-1];
    }
}

int rangeSum(int L, int R){
    return prefixSum[R] - prefixSum[L-1];
}
```

## 2D Prefix Sum

$$ prefixSum[i][j] = sum(arr[0...i][0...j]) $$

**Example**:

```
Input: arr = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

Output: prefixSum = [[1, 3, 6], [5, 12, 21], [12, 27, 45]]
```

### Range Sum

Range sum of arr[L...R] can be calculated as:

$$rangeSum[L...R] = prefixSum[R] - prefixSum[L-1]$$

**Cpp Implementation:**

```cpp
const int N = 1e5 + 7;
int prefixSum[N][N]; // 1-based indexing

void calculatePrefixSum(int arr[][N], int n, int m){
    prefixSum[0][0] = 0; // For 1-based indexing

    for(int i = 1; i <= n; i++){
        for(int j = 1; j <= m; j++){
            prefixSum[i][j] = prefixSum[i-1][j] + prefixSum[i][j-1] - prefixSum[i-1][j-1] + arr[i-1][j-1];
        }
    }
}

int rangeSum(int r1, int c1, int r2, int c2){
    return prefixSum[r2][c2] - prefixSum[r1-1][c2] - prefixSum[r2][c1-1] + prefixSum[r1-1][c1-1];
}
```