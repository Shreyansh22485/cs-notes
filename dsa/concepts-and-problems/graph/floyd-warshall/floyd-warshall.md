# Floyd-Warshall Algorithm

- Multiple Source Shortest Path Algorithm.

The Floyd-Warshall algorithm is a dynamic programming algorithm used to find the shortest paths between all pairs of vertices in a weighted graph. It can handle both positive and negative edge weights, but it cannot handle graphs with negative weight cycles.

## Implementation

```cpp
// Implementation of Floyd-Warshall Algorithm
void floydWarshall(int graph[V][V]) {
    int dist[V][V];

    // Initialize the distance matrix with the input graph
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            dist[i][j] = graph[i][j];
        }
    }

    // Update the distance matrix using dynamic programming
    for (int k = 0; k < V; k++) {
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                if (dist[i][k] != INT_MAX && dist[k][j] != INT_MAX) {
                    dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j]);
                }
            }
        }
    }

    // Print the shortest distance matrix
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            if (dist[i][j] == INT_MAX) {
                cout << "INF ";
            } else {
                cout << dist[i][j] << " ";
            }
        }
        cout << endl;
    }
}
```
- **Time Complexity**: O(V^3), where V is the number of vertices in the graph.
- **Space Complexity**: O(V^2), where V is the number of vertices in the graph.

### Detecting Negative Weight Cycles
To detect negative weight cycles using the Floyd-Warshall algorithm, we can check the diagonal of the distance matrix after running the algorithm. If any of the diagonal elements (dist[i][i]) is negative, it indicates that there is a negative weight cycle in the graph.

```cpp
// Check for negative weight cycles
bool hasNegativeWeightCycle(int dist[V][V]) {
    for (int i = 0; i < V; i++) {
        if (dist[i][i] < 0) {
            return true;
        }
    }
    return false;
}
```