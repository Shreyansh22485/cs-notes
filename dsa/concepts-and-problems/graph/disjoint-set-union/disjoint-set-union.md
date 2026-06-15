# Disjoint Set Union (DSU)

Disjoint Sets are sets that do not have any elements in common. Disjoint Set Union (DSU) is a data structure that keeps track of a partition of a set into disjoint subsets. It supports two primary operations: `find` and `union`.
- `find(x)`: This operation returns the representative (or root) of the set containing element `x`. It helps determine which subset an element belongs to.
- `union(x, y)`: This operation merges the sets containing elements `x` and `y`. If `x` and `y` are already in the same set, this operation does nothing.

```cpp
class DisjointSetUnion {
private:
    vector<int> parent, rank, size;
public:
    DisjointSetUnion(int n) {
        parent.resize(n+1);
        rank.resize(n+1, 0);
        size.resize(n+1, 1);
        for (int i = 0; i <= n; i++) {
            parent[i] = i;
        }
    }

    int find(int node) {
        if (parent[node] == node) {
            return node;
        }
        return parent[node] = find(parent[node]); // Path compression
    }

    void unionByRank(int u, int v) {
        int rootU = find(u);
        int rootV = find(v);
        if (rootU != rootV) {
            if (rank[rootU] < rank[rootV]) { // The higher rank tree becomes the parent
                parent[rootU] = rootV;
            } else if (rank[rootU] > rank[rootV]) {
                parent[rootV] = rootU;
            } else {
                parent[rootV] = rootU;
                rank[rootU]++; // Increment rank of parent if both have the same rank
            }
        }
    }

    void unionBySize(int u, int v) {
        int rootU = find(u);
        int rootV = find(v);
        if (rootU != rootV) {
            if (size[rootU] < size[rootV]) { // The larger size tree becomes the parent
                parent[rootU] = rootV;
                size[rootV] += size[rootU]; 
            } else {
                parent[rootV] = rootU;
                size[rootU] += size[rootV]; // Update size of the new parent tree
            }
        }
    }
};
```
- **Path Compression**: This technique is used in the `find` operation to flatten the structure of the tree, making future `find` operations faster. When we find the representative of a set, we also update the parent of each node along the path to point directly to the representative.
- **Union by Rank**: This technique is used in the `union` operation to keep the tree flat. We attach the smaller tree under the root of the larger tree based on rank.
- **Union by Size**: Similar to union by rank, but instead of using rank, we use the size of the tree to determine which tree to attach under the other.

- Time Complexity: Both `find` and `union` operations have an amortized time complexity of O(α(n)), where α(n) is the inverse Ackermann function, which grows very slowly and is practically constant for all reasonable values of n.

## Applications of Disjoint Set Union
1. **Kruskal's Algorithm**: DSU is used to detect cycles while building a minimum spanning tree.
2. **Connected Components**: DSU can be used to find connected components in a graph
3. **Dynamic Connectivity**: DSU can be used to dynamically connect and query connectivity between elements.
4. **Union-Find Problems**: DSU is commonly used in problems that involve grouping elements and checking if they belong to the same group.