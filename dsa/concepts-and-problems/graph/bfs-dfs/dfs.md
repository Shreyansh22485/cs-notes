# DFS 

- Depth -> Recursion

```cpp
#include <bits/stdc++.h>
using namespace std;

void dfs(int node, unordered_map<int, vector<int>>& adjList, vector<bool>& visited) {
    visited[node] = true;
    cout << node << " "; // Process the node (e.g., print it)

    for (int &neighbor : adjList[node]) {
        if (!visited[neighbor]) {
            dfs(neighbor, adjList, visited);
        }
    }
}

int main() {
    int n, e;
    cout << "Enter number of vertices: ";
    cin >> n;
    cout << "Enter number of edges: ";
    cin >> e;

    unordered_map<int, vector<int>> adjList;

    cout << "Enter edges (u v):" << endl;
    for (int i = 0; i < e; i++) {
        int u, v;
        cin >> u >> v;
        adjList[u].push_back(v); // For directed graph
        adjList[v].push_back(u); // For undirected graph
    }

    vector<bool> visited(n, false);
    
    cout << "DFS Traversal:" << endl;
    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            dfs(i, adjList, visited);
        }
    }

    return 0;
}
```

- Space Complexity: O(n + e) due to the adjacency list and visited array.
- Time Complexity: O(n + e) for traversing all vertices and edges.

