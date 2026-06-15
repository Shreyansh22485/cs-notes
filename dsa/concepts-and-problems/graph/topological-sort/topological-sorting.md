# Topological Sorting

- Directed Acyclic Graph (DAG) is a directed graph with no cycles.
- Topological sorting is a linear ordering of vertices such that for every directed edge u -> v, vertex u comes before vertex v in the ordering.

## DFS Based Approach

- We can perform a DFS and push the vertices onto a stack after visiting all their neighbors. Finally, we can pop all elements from the stack to get the topological order.

```cpp
#include <bits/stdc++.h>
using namespace std;

void topologicalSortUtil(int node, unordered_map<int, vector<int>>& adjList, vector<bool>& visited, stack<int>& Stack) {
    visited[node] = true;

    for (int &neighbor : adjList[node]) {
        if (!visited[neighbor]) {
            topologicalSortUtil(neighbor, adjList, visited, Stack);
        }
    }

    Stack.push(node);
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
        adjList[u].push_back(v);
    }

    vector<bool> visited(n, false);
    stack<int> Stack;

    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            topologicalSortUtil(i, adjList, visited, Stack);
        }
    }

    cout << "Topological Sort: ";
    while (!Stack.empty()) {
        cout << Stack.top() << " ";
        Stack.pop();
    }
    cout << endl;

    return 0;
}
```

- Space Complexity: O(n + e) due to the adjacency list, visited array, and stack.
- Time Complexity: O(n + e) for traversing all vertices and edges.

## BFS Based Approach (Kahn's Algorithm)

- We can calculate the in-degree of each vertex and repeatedly remove vertices with zero in-degree, adding them to the topological order.

```cpp
# include <bits/stdc++.h>
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

    vector<int> topologicalOrder;
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        topologicalOrder.push_back(node);

        for (int &neighbor : adjList[node]) {
            inDegree[neighbor]--;
            if (inDegree[neighbor] == 0) {
                q.push(neighbor);
            }
        }
    }

    if (topologicalOrder.size() != n) {
        cout << "Graph has a cycle. Topological sort not possible." << endl;
    } else {
        cout << "Topological Sort: ";
        for (int &vertex : topologicalOrder) {
            cout << vertex << " ";
        }
        cout << endl;
    }

    return 0;
}
```