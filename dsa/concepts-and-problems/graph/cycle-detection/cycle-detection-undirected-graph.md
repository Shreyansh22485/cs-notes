# Cycle Detection in Undirected Graph

## DFS Approach

- In undirected graphs, we can simply keep track of the parent node while performing DFS. If we encounter a visited node that is not the parent, it means there is a cycle.

```cpp
#include <bits/stdc++.h>
using namespace std;

bool dfs(int node, int parent, unordered_map<int, vector<int>>& adjList, vector<bool>& visited) {
    visited[node] = true;

    for (int &neighbor : adjList[node]) {
        if (!visited[neighbor]) {
            if (dfs(neighbor, node, adjList, visited)) {
                return true;
            }
        } else if (neighbor != parent) {
            return true; // Cycle detected
        }
    }
    return false;
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
    
    bool hasCycle = false;
    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            if (dfs(i, -1, adjList, visited)) {
                hasCycle = true;
                break;
            }
        }
    }

    if (hasCycle) {
        cout << "Graph contains a cycle." << endl;
    } else {
        cout << "Graph does not contain a cycle." << endl;
    }

    return 0;
}
```

- Space Complexity: O(n + e) due to the adjacency list and visited array.
- Time Complexity: O(n + e) for traversing all vertices and edges.

## BFS Approach

- Similar to DFS, we can keep track of the parent node while performing BFS. If we encounter a visited node that is not the parent, it means there is a cycle.

```cpp
#include <bits/stdc++.h>
using namespace std;

bool bfs(int startNode, unordered_map<int, vector<int>>& adjList, vector<bool>& visited) {
    queue<pair<int, int>> q; // Pair of (node, parent)
    q.push({startNode, -1});
    visited[startNode] = true;

    while (!q.empty()) {
        int node = q.front().first;
        int parent = q.front().second;
        q.pop();

        for (int &neighbor : adjList[node]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push({neighbor, node});
            } else if (neighbor != parent) {
                return true; // Cycle detected
            }
        }
    }
    return false;
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
    
    bool hasCycle = false;
    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            if (bfs(i, adjList, visited)) {
                hasCycle = true;
                break;
            }
        }
    }

    if (hasCycle) {
        cout << "Graph contains a cycle." << endl;
    } else {
        cout << "Graph does not contain a cycle." << endl;
    }

    return 0;
}
```
- Space Complexity: O(n + e) due to the adjacency list and visited array.
- Time Complexity: O(n + e) for traversing all vertices and edges.

## Disjoint Set Union (Union-Find) Approach
- We can use the Disjoint Set Union (DSU) data structure to detect cycles in an undirected graph. If we find an edge that connects two vertices that are already in the same set, it means there is a cycle.

```cpp
#include <bits/stdc++.h>
using namespace std;
class DisjointSetUnion {
private:
    vector<int> parent, rank;
public:
    DisjointSetUnion(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for (int i = 0; i < n; i++) {
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
};

int main() {
    int n, e;
    cout << "Enter number of vertices: ";
    cin >> n;
    cout << "Enter number of edges: ";
    cin >> e;

    DisjointSetUnion dsu(n);
    bool hasCycle = false;

    cout << "Enter edges (u v):" << endl;
    for (int i = 0; i < e; i++) {
        int u, v;
        cin >> u >> v;
        if (u < v){ // To avoid processing the same edge twice in an undirected graph
            if (dsu.find(u) == dsu.find(v)) {
                        hasCycle = true; // Cycle detected
                        break;
                    }
            dsu.unionByRank(u, v);
        }
        
    }

    if (hasCycle) {
        cout << "Graph contains a cycle." << endl;
    } else {
        cout << "Graph does not contain a cycle." << endl;
    }

    return 0;
}
```

- Space Complexity: O(n) for the DSU data structure.
- Time Complexity: O(e * α(n)) for processing all edges, where α(n) is the inverse Ackermann function, which is very slow-growing and can be considered almost constant for practical purposes.