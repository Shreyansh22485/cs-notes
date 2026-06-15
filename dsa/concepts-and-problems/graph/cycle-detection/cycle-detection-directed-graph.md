# Cycle Detection in Directed Graph

## DFS Based Approach

- In directed graphs, we need to keep track of the recursion stack to detect cycles. If we encounter a vertex that is already in the recursion stack in current recursion, it means there is a cycle.

```cpp
#include <bits/stdc++.h>
using namespace std;

bool dfs(int node, unordered_map<int, vector<int>>& adjList, vector<bool>& visited, vector<bool>& recStack) {
    visited[node] = true;
    recStack[node] = true;

    for (int &neighbor : adjList[node]) {
        if (!visited[neighbor]) {
            if (dfs(neighbor, adjList, visited, recStack)) {
                return true;
            }
        } else if (recStack[neighbor]) {
            return true; // Cycle detected
        }
    }

    recStack[node] = false;
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
    }

    vector<bool> visited(n, false);
    vector<bool> recStack(n, false);

    bool hasCycle = false;
    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            if (dfs(i, adjList, visited, recStack)) {
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

- Space Complexity: O(n) due to the visited and recursion stack arrays.
- Time Complexity: O(n + e) for traversing all vertices and edges.

## BFS Based Approach (Kahn's Algorithm)

- We can use Kahn's algorithm for topological sorting to detect cycles in a directed graph. If we cannot include all vertices in the topological order, it indicates the presence of a cycle.

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, e;
    cout << "Enter number of vertices: ";
    cin >> n;
    cout << "Enter number of edges: ";
    cin >> e;

    unordered_map<int, vector<int>> adjList;
    vector<int> inDegree(n, 0);

    cout << "Enter edges (u v):" << endl;
    for (int i = 0; i < e; i++) {
        int u, v;
        cin >> u >> v;
        adjList[u].push_back(v);
        inDegree[v]++;
    }

    queue<int> q;
    for (int i = 0; i < n; i++) {
        if (inDegree[i] == 0) {
            q.push(i);
        }
    }

    int count = 0;
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        count++;

        for (int &neighbor : adjList[node]) {
            inDegree[neighbor]--;
            if (inDegree[neighbor] == 0) {
                q.push(neighbor);
            }
        }
    }

    if (count != n) {
        cout << "Graph contains a cycle." << endl;
    } else {
        cout << "Graph does not contain a cycle." << endl;
    }

    return 0;
}
```