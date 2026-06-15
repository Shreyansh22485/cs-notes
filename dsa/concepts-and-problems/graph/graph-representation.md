# Adjacency Matrix Representation of Graphs

```cpp
#include <iostream>
using namespace std;

int main() {
    int n, e;
    cout << "Enter number of vertices: ";
    cin >> n;
    cout << "Enter number of edges: ";
    cin >> e;

    int adjMatrix[n][n] = {0};

    cout << "Enter edges (u v):" << endl;
    for (int i = 0; i < e; i++) {
        int u, v;
        cin >> u >> v;
        adjMatrix[u][v] = 1; // For directed graph
        adjMatrix[v][u] = 1; // For undirected graph
    }

    cout << "Adjacency Matrix:" << endl;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << adjMatrix[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}
```

- Space Complexity: O(n^2)
- Time Complexity: O(1) for edge lookup, O(n) for iterating through neighbors of a vertex.

# Adjacency List Representation of Graphs

```cpp
#include <bits/>stdc++.h>
using namespace std;

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

    cout << "Adjacency List:" << endl;
    for (auto &pair : adjList) {
        cout << pair.first << ": ";
        for (int neighbor : pair.second) {
            cout << neighbor << " ";
        }
        cout << endl;
    }
}
```

- Space Complexity: O(n + e)
- Time Complexity: O(k) for edge lookup, where k is the degree of the vertex, O(n) for iterating through all vertices.

