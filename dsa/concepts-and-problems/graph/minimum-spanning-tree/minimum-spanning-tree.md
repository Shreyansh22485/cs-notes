# Minimum Spanning Tree

- A **spanning tree** of a graph is a subgraph that is a tree and connects all the vertices together.
    - Graph(G) = (V, E) where V is the set of vertices and E is the set of edges.
    - It has all the vertices of the graph G
    - It has minimum possible number of edges, which is |V| - 1.

- A **minimum spanning tree (MST)** is a spanning tree with weight less than or equal to the weight of every other spanning tree. The weight of a spanning tree is the sum of weights given to each edge of the spanning tree.


## Prim's Algorithm

Prim's algorithm is a greedy algorithm that finds a minimum spanning tree for a connected weighted graph. It starts with an arbitrary vertex and grows the tree one edge at a time by adding the minimum weight edge that connects a vertex in the tree to a vertex outside the tree.

- Since we need to find the minimum weight edge at each step, we can use a priority queue (min-heap) to efficiently get the next edge with the smallest weight.
- We need to put three things in the priority queue:
    1. The weight of the edge [weight]
    2. The vertex that the edge connects to [node]
    3. The vertex that the edge is coming from [parent]
    - We also need to keep track of the vertices that are already included in the MST to avoid cycles.
    - We may also need to store the parent of each vertex to reconstruct the MST at the end.
    
### The algorithm can be summarized as follows:
1. Initialize a priority queue (min-heap) and add the starting vertex with weight 0 and no parent.
2. While the priority queue is not empty:
    - Extract the vertex with the minimum weight from the priority queue.
    - If the vertex has already been included in the MST, skip it.
    - Otherwise, add the vertex to the MST and update the total weight of the MST.
    - For each adjacent vertex of the extracted vertex, if it is not already in the MST, add it to the priority queue with its edge weight and parent information.

##### Code Implementation of Prim's Algorithm:

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, m;
    cin >> n >> m; // number of vertices and edges
    vector<pair<int, int>> adj[n]; // adjacency list

    for (int i = 0; i < m; i++) {
        int u, v, w;
        cin >> u >> v >> w; // edge from u to v with weight w
        adj[u].push_back({v, w});
        adj[v].push_back({u, w}); // undirected graph
    }

    vector<bool> inMST(n, false); // to keep track of vertices included in MST
    vector<int> parent(n, -1); // to store the parent of each vertex in MST
    priority_queue<pair<int, pair<int, int>>, vector<pair<int, pair<int, int>>>, greater<pair<int, pair<int, int>>>> pq; // min-heap
    pq.push({0, {0, -1}}); // starting with vertex 0

    int totalWeight = 0;

    while (!pq.empty()) {
        auto [weight, nodeInfo] = pq.top();
        pq.pop();
        int node = nodeInfo.first;
        int parentNode = nodeInfo.second;

        if (inMST[node]) continue; // skip if already included in MST

        inMST[node] = true; // include the vertex in MST
        totalWeight += weight; // add the weight to total weight
        parent[node] = parentNode; // set the parent of the vertex

        for (auto &[adjNode, edgeWeight] : adj[node]) {
            if (!inMST[adjNode]) {
                pq.push({edgeWeight, {adjNode, node}}); // add adjacent vertices to the priority queue
            }
        }
    }
    cout << totalWeight << endl; // print the total weight of the MST
    // MST can be reconstructed using the parent array

    vector<pair<int, int>> mstEdges;
    for (int i = 1; i < n; i++) {
        if (parent[i] != -1) {
            mstEdges.push_back({parent[i], i}); // store the edges of the MST
        }
    }
    // print the edges of the MST
    for (const auto &[u, v] : mstEdges) {
        cout << u << " " << v << endl;
    }

    return 0;
}
```
- Time Complexity: O(E log V), where E is the number of edges and V is the number of vertices.
- Space Complexity: O(V + E) for storing the graph and the priority queue.

## Kruskal's Algorithm

Kruskal's algorithm is another greedy algorithm that finds a minimum spanning tree for a connected weighted graph. It works by sorting all the edges in non-decreasing order of their weight and adding them one by one to the MST, ensuring that no cycles are formed.

### The algorithm can be summarized as follows:
1. Sort all the edges in non-decreasing order of their weight.
2. Initialize a disjoint-set (union-find) data structure to keep track of connected components.
3. For each edge in the sorted list:
    - If the edge connects two different components (i.e., it does not form a cycle), add it to the MST and union the two components.
    - If the edge connects two vertices that are already in the same component, skip it.

##### Code Implementation of Kruskal's Algorithm:
```cpp
#include <bits/stdc++.h>
using namespace std;

class DisjointSet {
    vector<int> parent, rank;

public:
    DisjointSet(int n) {
        parent.resize(n);
        rank.resize(n, 0);
        for (int i = 0; i < n; i++) {
            parent[i] = i; // each vertex is its own parent initially
        }
    }

    int find(int node){
        if(parent[node] == node) return node;
        return parent[node] = find(parent[node]); // path compression
    }

    void unionByRank(int u, int v){
        int rootU = find(u);
        int rootV = find(v);
        if(rootU != rootV){
            if(rank[rootU] < rank[rootV]){
                parent[rootU] = rootV;
            } else if(rank[rootU] > rank[rootV]){
                parent[rootV] = rootU;
            } else {
                parent[rootV] = rootU;
                rank[rootU]++;
            }
        }
    }
};

int main() {
    int n, m;
    cin >> n >> m; // number of vertices and edges
    vector<tuple<int, int, int>> edges; // (weight, u, v)

    for (int i = 0; i < m; i++) {
        int u, v, w;
        cin >> u >> v >> w; // edge from u to v with weight w
        edges.push_back({w, u, v});
    }

    sort(edges.begin(), edges.end()); // sort edges by weight

    DisjointSet ds(n);
    vector<pair<int, int>> mstEdges;
    int totalWeight = 0;

    for (auto &[weight, u, v] : edges) {
        if (ds.find(u) != ds.find(v)) { // if u and v are in different components
            ds.unionByRank(u, v); // union the components
            mstEdges.push_back({u, v}); // add edge to MST
            totalWeight += weight; // add weight to total weight
        }
    }

    cout << totalWeight << endl; // print the total weight of the MST
    // print the edges of the MST
    for (const auto &[u, v] : mstEdges) {
        cout << u << " " << v << endl;
    }

    return 0;
}
```
- Time Complexity: O(E log E + E α(V)), where E is the number of edges, V is the number of vertices, and α is the inverse Ackermann function.
- Space Complexity: O(V + E) for storing the graph and the disjoint-set data structure.