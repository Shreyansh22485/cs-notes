# Lowest Common Ancestor (LCA) using Binary Lifting

- We will keep jumping decreasing powers of 2 to reach the ancestors of those nodes until we find them unequal. 
If they are unequal , we will update the nodes to their ancestors and repeat the process.
- After this process, we will reach just below the LCA and we can return the parent of either of the nodes as the LCA.

**Note**: This method is only applicable when the nodes are at the same depth. If they are not at the same depth, we will first bring them to the same depth by jumping to their difference in depth and then making the lower node jump to the same depth as the higher node. After that, we can apply the above method to find the LCA.

```cpp
void findLCA(int u, int v) {
    if(depth[u] < depth[v]) swap(u, v); // Ensure u is the deeper node

    // Step 1: Bring u and v to the same depth
    int diff = depth[u] - depth[v];
    for(int j = 0; j < log2(n) + 1; j++) {
        if(diff & (1 << j)) {
            u = ancestorTable[u][j]; // Jump up by 2^j
        }
    }

    if(u == v) return u; // If they are the same, return one of them as LCA

    // Step 2: Jump upwards until we find reach just below the LCA
    for(int j = log2(n); j >= 0; j--) {
        if(ancestorTable[u][j] == -1) continue; // If there is no ancestor at this level, skip
        if(ancestorTable[u][j] != ancestorTable[v][j]) {
            u = ancestorTable[u][j]; // Jump up by 2^j
            v = ancestorTable[v][j]; // Jump up by 2^j
        }
    }

    return ancestorTable[u][0]; // Return the parent of either node as LCA
}
```
- Time Complexity: O(log n) for each LCA query after O(n log n) preprocessing time.
- Space Complexity: O(n log n) for the ancestorTable array.