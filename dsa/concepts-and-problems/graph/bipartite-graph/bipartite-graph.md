# Bipartite Graph

A bipartite graph is a graph whose vertices can be divided into two disjoint sets such that no two vertices within the same set are adjacent. In other words, if we can color the graph using two colors such that no two adjacent vertices share the same color, then the graph is bipartite.

- odd-length cycles are not bipartite, while even-length cycles are bipartite.

### When to use bipartite graphs?
- Dividing (Grouping) a set of objects into two distinct sets based on some relationship.


## DFS Based Approach
- We can use DFS to try to color the graph with two colors. If we find a conflict in coloring, it means the graph is not bipartite.

```cpp
bool isBipartite(int node, vector<int> adj[], vector<int>& color, int currentColor) {
    color[node] = currentColor;
    for (int neighbor : adj[node]) {
        if (color[neighbor] == -1) {
            if (!isBipartite(neighbor, adj, color, 1 - currentColor)) {
                return false;
            }
        } else if (color[neighbor] == currentColor) {
            return false; // Conflict in coloring
        }
    }
    return true;
}

```
- Time Complexity: O(V + E), where V is the number of vertices and E is the number of edges.
- Space Complexity: O(V) for the color array and recursion stack in the worst case.

## BFS Based Approach
- Similar to DFS, we can use BFS to color the graph. We start from an unvisited vertex, color it, and then color all its neighbors with the opposite color. If we find a conflict in coloring, the graph is not bipartite.

```cpp
bool isBipartiteBFS(int startNode, vector<int> adj[], vector<int>& color) {
    queue<int> q;
    q.push(startNode);
    color[startNode] = 0; // Start coloring with 0
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        for (int neighbor : adj[node]) {
            if (color[neighbor] == -1) {
                color[neighbor] = 1 - color[node]; // Color with opposite color
                q.push(neighbor);
            } else if (color[neighbor] == color[node]) {
                return false; // Conflict in coloring
            }
        }
    }
    return true;
}
```
- Time Complexity: O(V + E), where V is the number of vertices and E is the number of edges.
- Space Complexity: O(V) for the color array and queue in the worst case.