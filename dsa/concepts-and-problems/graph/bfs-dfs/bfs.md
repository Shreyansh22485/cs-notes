# BFS

- Level order traversal of a graph.
- Shortest path in an unweighted graph.
- Shortest path in a weighted graph with all edges having the same weight.

```cpp
#include <bits/stdc++.h>
using namespace std;

void bfs(int startNode, unordered_map<int, vector<int>>& adjList, vector<bool>& visited) {
    queue<int> q;
    q.push(startNode);
    visited[startNode] = true;

    while (!q.empty()) {
        int node = q.front();
        q.pop();
        cout << node << " "; // Process the node (e.g., print it)

        for (int &neighbor : adjList[node]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
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
    
    cout << "BFS Traversal:" << endl;
    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            bfs(i, adjList, visited);
        }
    }

    return 0;
}
```

- Space Complexity: O(n + e) due to the adjacency list and visited array.
- Time Complexity: O(n + e) for traversing all vertices and edges.



### Second Form of BFS

```cpp
#include <bits/stdc++.h>
using namespace std;

void bfs(int startNode, unordered_map<int, vector<int>>& adjList, vector<bool>& visited) {
    queue<int> q;
    q.push(startNode);
    visited[startNode] = true;
    int level = 0;
    while (!q.empty()) {
        int size = q.size();
        while(size--) {
            int node = q.front();
            q.pop();
            cout << node << " "; // Process the node (e.g., print it)

            for (int &neighbor : adjList[node]) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    q.push(neighbor);
                }
            }
        }
        level++;
    }
}
```
- Use of first version of BFS is for simple traversal, while the second version is useful for level order traversal, where we want to process nodes level by level.

