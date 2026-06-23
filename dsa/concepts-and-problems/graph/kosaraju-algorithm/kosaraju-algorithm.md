# Kosaraju's Algorithm

## Strongly Connected Components (SCC)

A strongly connected component (SCC) in a directed graph is a maximal subgraph where every pair of vertices is connected by a path in both directions.

## Intuition
- **Why Reverse the Graph?**: Because if we reverse all the edges in the graph, the edge that was going outward from a SCC will now be going inward therefore while performing DFS on the reversed graph, we can reach all the vertices in that SCC. Note that the reversal has no effect on the SCC edges as they still remain reachable from each other.

- **Why DFS on Topological Order?**: Because there is a dependency that one node of a SCC has to be visited before the another node of other SCC. So topological order gives us the order in which we can visit the nodes of the graph such that we can reach all the nodes of a SCC before moving to another SCC. This order process nodes in decreasing finishing time order.

### The algorithm can be summarized as follows:
1. Perform a DFS on the original graph and store the vertices in a stack according to their finishing times (i.e., push the vertex onto the stack after all its neighbors have been visited). 
2. Reverse the graph (i.e., reverse the direction of all edges).
3. While the stack is not empty, pop a vertex from the stack and perform a DFS on the reversed graph starting from that vertex. The set of vertices reached in this DFS forms a strongly connected component (SCC). Repeat this process until the stack is empty.

## C++ Implementation

```cpp
#include <bits/stdc++.h>
using namespace std;

const int N = 1e5 + 5;
vector<int> adj[N];
vector<int> rev_adj[N];
bool visited[N];
stack<int> st;

void dfs(int u) {
    visited[u] = true;
    for (int v : adj[u]) {
        if (!visited[v]) {
            dfs(v);
        }
    }
    st.push(u);
}

void dfs_rev(int u, vector<int>& component) {
    visited[u] = true;
    component.push_back(u);
    for (int v : rev_adj[u]) {
        if (!visited[v]) {
            dfs_rev(v, component);
        }
    }
}

int main() {
    int n, m;
    cin >> n >> m;
    
    for (int i = 0; i < m; i++) {
        int u, v;
        cin >> u >> v;
        adj[u].push_back(v);
        rev_adj[v].push_back(u);
    }

    // Step 1: Perform DFS on original graph and store vertices in stack
    for (int i = 1; i <= n; i++) {
        if (!visited[i]) {
            dfs(i);
        }
    }

    // Step 2: Reset visited array
    memset(visited, false, sizeof(visited));

    // Step 3: Process vertices in reverse topological order
    while (!st.empty()) {
        int u = st.top();
        st.pop();
        if (!visited[u]) {
            vector<int> component;
            dfs_rev(u, component);
            // Print the strongly connected component
            for (int v : component) {
                cout << v << " ";
            }
            cout << "\n";
        }
    }

    return 0;
}
```
- Time Complexity: O(V + E), where V is the number of vertices and E is the number of edges in the graph.
- Space Complexity: O(V + E) for storing the graph and the stack.

*Note That This is not exactly Topological Sort because Topological Sort is only applicable to Directed Acyclic Graphs (DAGs), while Kosaraju's Algorithm can be applied to any directed graph, including those with cycles.*