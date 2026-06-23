# Bellman-Ford Algorithm

## Drawbacks of Dijkstra's Algorithm
- Cannot handle negative weight edges.
- Cannot detect negative weight cycles. (A Cycle is a negative weight cycle if the sum of the weights of the edges in the cycle is negative.)

## Bellman-Ford Algorithm
- It will work only for directed graphs.
- If undirected graph is given, we can convert it into directed graph by replacing each undirected edge with two directed edges in opposite directions, but it will not work if there are negative weight edges in the undirected graph.


It says if there are v vertices and e edges, then the shortest path from the source vertex to all other vertices can be found in O(v*e) time by relaxing all the edges v-1 times.  

- **Relaxation**: Relaxation is the process of updating the distance of a vertex if a shorter path is found. For an edge (u, v) with weight w, if the distance to u plus w is less than the distance to v, then we update the distance to v.  
  - Mathematically, if dist[u] + w < dist[v], then we update dist[v] = dist[u] + w. provided that dist[u] is not infinity.

- **Why v-1 times?**  
  The shortest path from the source vertex to any other vertex can have at most v-1 edges. Therefore, we need to relax all the edges v-1 times to ensure that we have found the shortest path to all vertices.

### Algorithm
1. Initialize the distance to the source vertex as 0 and all other vertices as infinity.
2. Repeat the following steps v-1 times:
   - For each edge (u, v) with weight w, perform relaxation: if dist[u] != infinity and dist[u] + w < dist[v], then update dist[v] = dist[u] + w.
3. After v-1 iterations, check for negative weight cycles by iterating through all edges again. If we can still relax any edge, then there is a negative weight cycle in the graph.

```cpp
// Implementation of Bellman-Ford Algorithm
void bellmanFord(int src, vector<Edge> edges, int v) {
    vector<int> dist(v, INT_MAX);
    dist[src] = 0;

    // Relax all edges v-1 times
    for (int i = 0; i < v - 1; i++) {
        for (auto edge : edges) {
            int u = edge.u;
            int v = edge.v;
            int w = edge.w;
            if (dist[u] != INT_MAX && dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
            }
        }
    }

    // Check for negative weight cycles
    for (auto edge : edges) {
        int u = edge.u;
        int v = edge.v;
        int w = edge.w;
        if (dist[u] != INT_MAX && dist[u] + w < dist[v]) {
            cout << "Graph contains negative weight cycle" << endl;
            return;
        }
    }

    // Print the shortest distances
    for (int i = 0; i < v; i++) {
        cout << "Distance from source to vertex " << i << " is " << dist[i] << endl;
    }
}
```
- Time Complexity: O(v*e), where v is the number of vertices and e is the number of edges in the graph. We relax all edges v-1 times, and then check for negative weight cycles in O(e) time.
- Space Complexity: O(v), where v is the number of vertices in the graph. We use an array to store the shortest distances from the source vertex to all other vertices.
