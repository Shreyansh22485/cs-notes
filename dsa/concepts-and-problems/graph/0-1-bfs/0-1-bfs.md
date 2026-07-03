# 0-1 BFS

- Variation of Simple BFS
- Used to find single source shortest path to all nodes in a weighted graph
- Weights are either 0 or 1

---

### In normal BFS
- Each edge has same weight
- Queue has at max two levels

---

## Algorithm

1. Initialize dist[] array with -1
2. Initialize deque
3. Push source node in deque
4. While deque is not empty
    - Remove front node from deque
    - For each neighbor of front node
        - If neighbor is not visited
            - Mark neighbor as visited
            - If weight is 0
                - Push neighbor to front of deque
            - Else
                - Push neighbor to back of deque



## C++ Implementation

```cpp
#include <iostream>
#include <vector>
#include <deque>

using namespace std;

void 01BFS(int src, int V, vector<vector<pair<int, int>>>& adj) {
    vector<int> dist(V, 1e9);
    deque<int> dq;

    dist[src] = 0;
    dq.push_front(src);

    while (!dq.empty()) {
        int u = dq.front();
        dq.pop_front();

        for (auto& edge : adj[u]) {
            int v = edge.first;
            int weight = edge.second;

            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                if (weight == 0) {
                    dq.push_front(v);
                } else {
                    dq.push_back(v);
                }
            }
        }
    }
}
```

## Time Complexity

- O(V + E)

## Space Complexity

- O(V)

