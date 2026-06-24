# Multi-Source BFS

Multi-source BFS is a variation of the standard BFS algorithm where we start the search from multiple source nodes simultaneously. This approach is useful when we want to find the shortest distance from any of several starting points to all other nodes in the graph.

- Starts simultaneously from multiple source nodes.
- Useful when you want to spread outwards from multiple points at once.

*When you need to compute shortest distance/minimum cost/minimum time from multiple sources to all other nodes in a graph, multi-source BFS is the right choice.*

Multi-Source BFS ensures that all nodes are reached with the **minimum** steps/time from the **nearest** source node.

## Algorithm
1. Initialize a queue and enqueue all source nodes.
2. Mark all source nodes as visited and set their distance to 0.
3. While the queue is not empty:
   - Dequeue a node from the queue.
   - For each unvisited neighbor of the dequeued node:
     - Mark it as visited.
     - Set its distance to the distance of the dequeued node + 1.
     - Enqueue the neighbor.

