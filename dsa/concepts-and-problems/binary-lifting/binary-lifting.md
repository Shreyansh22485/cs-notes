# Binary Lifting (DP on Trees)

## Introduction

- It helps to jump upwards in a tree in logarithmic time.
- We jump in powers of 2, i.e., 1, 2, 4, 8, etc. because any number can be represented as a sum of powers of 2.
- We can find the 2^i-th ancestor of a node in O(1) time after O(n log n) preprocessing time.

### How to store powers of 2 jumps information?

- We can use a 2D array `ancestorTable[node][i]` where `ancestorTable[node][i]` stores that if we jump 2^i times from `node`, where do we end up? 
- `ancestorTable[node][i]` = 2^i-th ancestor of `node`.

```
2^j = 2^(j-1) + 2^(j-1)
a = ancestorTable[node][j-1] // 2^(j-1) ancestor of node
ancestorTable[node][j] = ancestorTable[a][j-1] // 2^(j-1) ancestor of a
```
$$
ancestorTable[node][j] = ancestorTable[ancestorTable[node][j-1]][j-1];
$$
$$
ancestorTable[][] \leftarrow \text{Rows} = \text{nodes}, \quad \text{Columns} = \log_2(n) +1
$$ 

## Code Snippet

Building the ancestorTable array for binary lifting:

```cpp
for(int j = 1; j < log2(n)+1; j++){
    for(int node = 0; node < n; node++){
        if(ancestorTable[node][j-1] != -1){
            ancestorTable[node][j] = ancestorTable[ancestorTable[node][j-1]][j-1];
        }
    }
}
```
- We need to fill the first column (j=0) of the ancestorTable array with the immediate parent of each node via DFS.

## Finding the k-th ancestor of a node 

```cpp
for(int j = 0; j < log2(n)+1; j++){
    if(k & (1 << j)){
        node = ancestorTable[node][j];
        if(node == -1) break;
    }
}
```
- Time Complexity: O(log n) for each query after O(n log n) preprocessing time.
- Space Complexity: O(n log n) for the ancestorTable array.

