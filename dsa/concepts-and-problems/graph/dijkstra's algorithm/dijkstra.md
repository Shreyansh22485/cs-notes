# Dijkstra's Algorithm

Dijkstra's algorithm is a popular algorithm used to find the shortest path from a source vertex to all other vertices in a weighted graph. 

## Using Priority Queue (Min-Heap)

```cpp
#include <bits/stdc++.h>
using namespace std;

void dijkstra(int V, vector<pair<int,int>> adj[], int S) {
    vector<int> dist(V, INT_MAX);
    dist[S] = 0;
    priority_queue<pair<int,int>, vector<pair<int,int>>, greater<pair<int,int>>> pq;
    pq.push({0, S});

    while (!pq.empty()) {
        int distance = pq.top().first;
        int node = pq.top().second;
        pq.pop();

        for (auto &neighbor : adj[node]) {
            int nextNode = neighbor.first;
            int weight = neighbor.second;

            if (distance + weight < dist[nextNode]) {
                dist[nextNode] = distance + weight;
                pq.push({dist[nextNode], nextNode});
            }
        }
    }
    // Print distances from source
    for (int i = 0; i < V; i++) {
        cout << "Distance from source " << S << " to vertex " << i << " is " << dist[i] << endl;
    }
}
```

- Time Complexity: O((V + E) log V) where V is the number of vertices and E is the number of edges.
- Space Complexity: O(V) for the distance array and the priority queue.

## Using Set

```cpp
#include <bits/stdc++.h>
using namespace std;

void dijkstra(int V, vector<pair<int,int>> adj[], int S) {
    vector<int> dist(V, INT_MAX);
    dist[S] = 0;
    set<pair<int,int>> st;
    st.insert({0, S});

    while (!st.empty()) {
        auto it = st.begin();
        int distance = it->first;
        int node = it->second;
        st.erase(it);

        for (auto &neighbor : adj[node]) {
            int nextNode = neighbor.first;
            int weight = neighbor.second;

            if (distance + weight < dist[nextNode]) {
                if (dist[nextNode] != INT_MAX) {
                    st.erase({dist[nextNode], nextNode});
                }
                dist[nextNode] = distance + weight;
                st.insert({dist[nextNode], nextNode});
            }
        }
    }
    // Print distances from source
    for (int i = 0; i < V; i++) {
        cout << "Distance from source " << S << " to vertex " << i << " is " << dist[i] << endl;
    }
}
```
- Time Complexity: O((V + E) log V) where V is the number of vertices and E is the number of edges.
- Space Complexity: O(V) for the distance array and the set.
- Set enables an explicit decrease-key via erase/insert (and typically keeps the container size closer to V), but has higher constant factors and more expensive tree operations than a heap-based priority_queue approach.

## Why not use a simple queue?
We cannot use a simple queue because Dijkstra's algorithm requires that we always process the vertex with the smallest distance next. A simple queue does not guarantee this order, which can lead to incorrect results. The priority queue or set ensures that we always expand the least-cost node first, maintaining the correctness of the algorithm.

### Mathematical Proof of Time Complexity:

O(V * (pop vertex from priority queue + number of edges on each vertex * push into priority queue))
= O(V * (log of heap size)(1 + number of edges on each vertex))
= O(V * (log of heap size)(1 + V-1))
= O(V * V * log of heap size)
= O(V^2 * log of heap size)
= O(V^2 * log V*V)
= O(V^2 * 2*log V)
= O(V^2 * log V)
= O(E * log V) (since E can be at most V^2 in a dense graph)