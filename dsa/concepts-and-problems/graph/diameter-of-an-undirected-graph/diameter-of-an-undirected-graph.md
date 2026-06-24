# Diameter of an Undirected Graph

The diameter of an undirected graph is the longest shortest path between any two vertices in the graph. This path does not contain any repeated vertices or edges. 

*If you choose a random node (u) and find the farthest node (v) from it, then this node (v) will be one of the endpoints of the diameter. Then, if you find the farthest node from (v), you will get the other endpoint of the diameter.*

## Algorithm
1. Pick a random node (u) and find the farthest node (v) from it using BFS or DFS.
2. Find the farthest node (w) from (v) using BFS or DFS.
3. The distance between (v) and (w) is the diameter of the graph.

### C++ Implementation of Diameter of an Undirected Graph

```cpp
#include <bits/stdc++.h>
using namespace std;

unordered_map<int, vector<int>> adj;
vector<bool> visited;

pair<int, int> bfs(int start) {
    queue<int> q;
    q.push(start);
    visited[start] = true;
    int farthestNode = start;
    int level = 0;

    while (!q.empty()) {
        int size = q.size();
        while (size--) {
            int node = q.front();
            q.pop();
            farthestNode = node;

            for (int neighbor : adj[node]) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    q.push(neighbor);
                }
            }
        }
    }

    return {farthestNode, level};
}

int main() {
    int n, m;
    cin >> n >> m;
    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
        adj[v].push_back(u);
    }
    visited.resize(n + 1, false);
    pair<int, int> farthestNode = bfs(1); // Start BFS from node 1
    fill(visited.begin(), visited.end(), false); // Reset visited for the second BFS
    pair<int, int> otherFarthestNode = bfs(farthestNode.first); // Find the farthest node from the first farthest node 

    cout << "One endpoint of the diameter: " << farthestNode.first << endl;
    cout << "Other endpoint of the diameter: " << otherFarthestNode.first << endl;
    cout << "Diameter of the graph: " << otherFarthestNode.second << endl; // level will give the diameter

    return 0;
}
```
- Time Complexity: O(V + E), where V is the number of vertices and E is the number of edges in the graph.
- Space Complexity: O(V + E) for storing the adjacency list and O(V) for the visited array.