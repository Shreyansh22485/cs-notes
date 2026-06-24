# Euler Path and Circuit

An **Euler Path** in a graph is a path that visits every edge exactly once. An **Euler Circuit** is an Euler Path that starts and ends at the same vertex.

*Note*
- Not all graphs have an Euler Path or Circuit. The existence of these paths depends on the degrees of the vertices in the graph.
- Be careful from which node you start your eulerian path.

---

- If the graph does not hvae Eulerian Circuit:-
    - Either you wont be alle to to come back to the starting node 
    - or, you will not be able to visit all the edges in the graph.
- All vertices **with non-zero degree need to belong to a single connected component** for an Euler Path or Circuit to exist.

## Degree Conditions
- **Euler Circuit**: A connected graph has an Euler Circuit if and only if **every** vertex has an **even** degree.
- **Euler Path**: A connected graph has an Euler Path if and only if **exactly zero** or two vertices (**start and end**) have an **odd** degree.

*If a graph has Euler Path but not Euler Circuit, then it is called Semi-Eulerian Graph.*

## Detecting Euler Path and Circuit
1. Check if the graph is connected (ignoring vertices with zero degree).
2. Count the number of vertices with odd degree.
3. If the count is 0, then the graph has an Euler Circuit.
4. If the count is 2, then the graph has an Euler Path.
5. If the count is greater than 2, then the graph has neither an Euler Path nor an Euler Circuit.

### C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100005;
vector<int> adj[MAX];
bool visited[MAX];

void dfs(int u) {
    visited[u] = true;
    for (int v : adj[u]) {
        if (!visited[v]) {
            dfs(v);
        }
    }
}

bool isConnected() {
    fill(visited, visited + MAX, false);
    int start = -1;
    for (int i = 1; i <= n; i++) {
        if (adj[i].size() > 0) { // Find a vertex with non-zero degree
            start = i;
            break;
        }
    }
    if (start == -1) return true;
    dfs(start);

    // check if all vertices with non-zero degree are visited
    for (int i = 1; i <= n; i++) {
        if (adj[i].size() > 0 && !visited[i]) {
            return false;
        }
    }
    return true;
}

bool hasEulerianPathOrCircuit() {
    if (!isConnected()) return false;

    int oddCount = 0;
    for (int i = 1; i <= n; i++) {
        if (adj[i].size() % 2 == 1) {
            oddCount++;
        }
    }

    if (oddCount == 0) {
        cout << "Eulerian Circuit exists." << endl;
        return true;
    } else if (oddCount == 2) {
        cout << "Eulerian Path exists." << endl;
        return true;
    } else {
        cout << "Neither Eulerian Path nor Circuit exists." << endl;
        return false;
    }
}
```
- Time Complexity: O(V + E), where V is the number of vertices and E is the number of edges in the graph.
- Space Complexity: O(V + E) for storing the adjacency list and O(V) for the visited array.


## Euler in Directed Graphs

In directed graphs, the concept of Eulerian paths and circuits is slightly different due to the direction of edges.

### Degree Conditions
- **Euler Circuit**: A strongly connected directed graph has an Euler Circuit if and only if **every** vertex has an **equal in-degree and out-degree**.
- **Euler Path**: A strongly connected directed graph has an Euler Path if and only if **exactly zero** or two vertices (**start and end**) have an **in-degree and out-degree difference exactly 1**.

*If a directed graph has an Euler Path but not an Euler Circuit, then it is called Semi-Eulerian Graph.*

### Detecting Euler Path and Circuit in Directed Graphs
1. Check if the graph is strongly connected (ignoring vertices with zero degree).
2. Count the number of vertices with unequal in-degree and out-degree.
3. If the count is 0, then the graph has an Euler Circuit.
4. If the count is 2, then the graph has an Euler Path.
5. If the count is greater than 2, then the graph has neither an Euler Path nor an Euler Circuit.

#### C++ Implementation of Euler Path and Circuit in Directed Graphs

```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
    int n, m;
    cin >> n >> m;

    vector<int> in_degree(n + 1, 0), out_degree(n + 1, 0);
    vector<vector<int>> adj(n + 1);

    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
        out_degree[u]++;
        in_degree[v]++;
    }

    // Check for Euler Path or Circuit
    int start_nodes = 0, end_nodes = 0;
    for (int i = 1; i <= n; i++) {
        if (out_degree[i] - in_degree[i] == 1) {
            start_nodes++;
        } else if (in_degree[i] - out_degree[i] == 1) {
            end_nodes++;
        } else if (in_degree[i] != out_degree[i]) {
            cout << "Neither Eulerian Path nor Circuit exists." << endl;
            return 0;
        }
    }

    if (start_nodes == 0 && end_nodes == 0){
        cout << "Eulerian Circuit exists." << endl;
    } else if (start_nodes == 1 && end_nodes == 1){
        cout << "Eulerian Path exists." << endl;
    } else {
        cout << "Neither Eulerian Path nor Circuit exists." << endl;
    }

    return 0;
}
```
- Time Complexity: O(V + E), where V is the number of vertices and E is the number of edges in the graph.
- Space Complexity: O(V + E) for storing the adjacency list and O(V) for the in-degree and out-degree arrays.

## Finding Euler Path in Directed Graphs
1. Find the starting vertex (the vertex with out-degree greater than in-degree by 1).
2. If all vertices have equal in-degree and out-degree, you can start from any vertex.
3. Use **Hierholzer's algorithm** to find the Euler Path or Circuit:
   - Start from the starting vertex and follow edges until you return to the starting vertex (for a circuit) or reach the end vertex (for a path).
   - If you reach a vertex with unused edges, continue from that vertex until all edges are used.

### C++ Implementation of Hierholzer's Algorithm

```cpp
#include <bits/stdc++.h>
using namespace std;

void findEulerPath(int u, vector<vector<int>>& adj, vector<int>& eulerPath) {
    while (!adj[u].empty()) {
        int v = adj[u].back(); // Get the last edge
        adj[u].pop_back(); // Remove the edge from the graph because we should visit it only once
        findEulerPath(v, adj, eulerPath);
    }
    eulerPath.push_back(u);
}

int main(){
    int n, m;
    cin >> n >> m;

    vector<vector<int>> adj(n + 1);
    vector<int> in_degree(n + 1, 0), out_degree(n + 1, 0);

    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
        out_degree[u]++;
        in_degree[v]++;
    }

    // Find starting vertex
    int start = 1;
    for (int i = 1; i <= n; i++) {
        if (out_degree[i] - in_degree[i] == 1) {
            start = i;
            break;
        }
    }

    vector<int> eulerPath;
    findEulerPath(start, adj, eulerPath);
    // Print the Euler Path
    for (int i = eulerPath.size() - 1; i >= 0; i--) { // Print in reverse order
        cout << eulerPath[i] << " ";
    }
    cout << endl;
}
```
- Time Complexity: O(V + E), where V is the number of vertices and E is the number of edges in the graph.
- Space Complexity: O(V + E) for storing the adjacency list and O(V) for the eulerPath vector.