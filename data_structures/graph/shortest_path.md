# Shortest Path

The Shortest Path Problem is a fundamental problem in graph theory. Given a weighted graph, the goal is to find the shortest path between two nodes (also known as vertices) that minimizes the sum of edge weights.

## Common Algorithms
- Dijkstra's Algorithm
- Bellman-Ford Algorithm

## Dijkstra's Algorithm

A greedy algorithm works by maintaining a priority queue of nodes, where the priority is the minimum distance from the source node to each node.

### Python Implementation
```python
import heapq

class Graph:
    def __init__(self, vertices):
        self.V = vertices  # Number of vertices
        self.edges = []    # List to store edges

    def add_edge(self, u, v, w):
        # Adds an edge to the graph (u, v, weight)
        self.edges.append((u, v, w))

    def dijkstra(self, src):
        # Initialize distances with infinity
        dist = [float('inf')] * self.V
        dist[src] = 0
        pq = [(0, src)]  # (distance, vertex) priority queue
        heapq.heapify(pq)

        while pq:
            u_dist, u = heapq.heappop(pq)

            # Skip if the current distance is not the latest
            if u_dist > dist[u]:
                continue

            # Relax edges
            for u_, v, w in self.edges:
                if u_ == u and dist[v] > dist[u] + w:
                    dist[v] = dist[u] + w
                    heapq.heappush(pq, (dist[v], v))

        return dist

# Example usage
g = Graph(5)
g.add_edge(0, 1, 4)
g.add_edge(0, 2, 3)
g.add_edge(1, 2, 2)
g.add_edge(1, 3, 10)
g.add_edge(2, 1, 8)
g.add_edge(2, 3, 5)
g.add_edge(3, 4, 7)

dist = g.dijkstra(0)

for i in range(5):
    print(f"Distance from node 0 to node {i}: {dist[i]}")
```

### Runtime Complexity

The time complexity of Dijkstra's Algorithm is **O(|E|log|V|)** in the worst case, where: |E| is the number of edges in the graph. |V| is the number of vertices (nodes) in the graph.

This is because the algorithm uses a priority queue to keep track of nodes to visit, and the priority queue operations (insertion and extraction) take O(log|V|) time. The loop iterates over all edges, so it takes O(|E|) time. Therefore, the total time complexity is **O(|E|log|V|)**.

## Bellman-Ford Algorithm: 

A modification of Dijkstra's Algorithm that handles negative weight edges. It's particularly useful for graphs with negative cycles, which can cause Dijkstra's Algorithm to fail.

### Python Implmentation
```python
import sys

class Graph:
    def __init__(self, vertices):
        self.V = vertices  # Number of vertices
        self.edges = []    # List to store edges

    def add_edge(self, u, v, w):
        # Adds an edge to the graph (u, v, weight)
        self.edges.append((u, v, w))

    def bellman_ford(self, src):
        # Initialize distance from source to all other vertices as infinity
        dist = [sys.maxsize] * self.V
        dist[src] = 0

        # Relax all edges |V-1| times
        for _ in range(self.V - 1):
            for u, v, w in self.edges:
                if dist[u] != sys.maxsize and dist[u] + w < dist[v]:
                    dist[v] = dist[u] + w

        # Check for negative weight cycles
        for u, v, w in self.edges:
            if dist[u] != sys.maxsize and dist[u] + w < dist[v]:
                print("Graph contains negative weight cycle")
                return None

        return dist

# Example usage
g = Graph(5)
g.add_edge(0, 1, -2)  # Negative weight edge
g.add_edge(1, 2, 3)   # Positive weight edge
g.add_edge(2, 3, 2)   # Positive weight edge
g.add_edge(3, 4, -1)  # Negative weight edge
g.add_edge(4, 0, 2)   # Positive weight edge

dist = g.bellman_ford(0)

if dist is not None:
    print("Shortest distances from node 0:")
    for i in range(g.V):
        print(f"Node {i}: {dist[i]}")
```

### Key points

- The algorithm can handle negative weight edges, which Dijkstra' s Algorithm cannot.
- It uses the same priority queue operations as Dijkstra' s Algorithm.
- The time complexity is **O(|E| * |V|)**, where |E| is the number of edges and |V| is the number of vertices.

## Leetcode Questions

| # | Problem | Difficulty |
|---|---------|------------|
| 787 | [Cheapest Flights Within K Stops](../../leetcode_questions/787_cheapest_flights_within_k_stops.md) | Medium |
