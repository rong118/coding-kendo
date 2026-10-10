# Minimum Spanning Tree

A Minimum Spanning Tree (MST) of a weighted, undirected graph is a spanning tree whose total edge weight is the minimum possible among all spanning trees of the graph.

The cost of the spanning tree is the sum of the weights of all the edges in the tree. There can be many spanning trees. Minimum spanning tree is the spanning tree where the cost is minimum among all the spanning trees. There also can be many minimum spanning trees.

## Key Concepts:

- **Graph**:

  A collection of vertices (or nodes) connected by edges. In the weighted graph, each edge has an associated numerical value (weight).

- **Spanning Tree**:

  A subgraph that includes all the vertices of the original graph, is connected and contains no cycles. Essentially, it "spans" all the vertices with the minimum number of edges.

- **Minimum Spanning Tree**:

  Among all possible spanning trees of a graph, the MST is the one with the smallest possible sum of edge weights.

## Find an MST:

There are several well-known algorithms for finding an MST in a graph:

- Kruskal's Algorithm
  
- Prim's Algorithm

## Kruskal's Algorithm:

Sort all the edges in the graph by increasing weight.
Add edges to the MST, in order of their weight, as long as they don't form a cycle with the already included edges.
Stop when the MST contains V−1 edges.

### Workflow of Kruskal's Algorithm:
- Initialization:

  Create a list of all edges in the graph, sorted by their weight. Initialize a data structure (typically a Disjoint Set Union/Find structure) to keep track of which vertices are in which components.

- Algorithm Execution:

  Iterate through the sorted edges, adding the smallest edge to the MST if it doesn't form a cycle with the already included edges. This is determined using the Union-Find data structure. Continue this process until the MST contains V−1 edges, where V is the number of vertices in the graph.

- Result:

  The edges added during the iteration that form the MST

### Implementation
```python
from typing import List, Tuple

class Edge:
    def __init__(self, src: int, dest: int, weight: int):
        self.src = src
        self.dest = dest
        self.weight = weight

    def __lt__(self, other):
        return self.weight < other.weight

class DisjointSet:
    def __init__(self, n: int):
        self.parent = list(range(n))
        self.rank = [0] * n

    def find(self, u: int) -> int:
        if self.parent[u] != u:
            self.parent[u] = self.find(self.parent[u])  # Path compression
        return self.parent[u]

    def union(self, u: int, v: int):
        root_u = self.find(u)
        root_v = self.find(v)

        if root_u != root_v:
            if self.rank[root_u] < self.rank[root_v]:
                self.parent[root_u] = root_v
            elif self.rank[root_u] > self.rank[root_v]:
                self.parent[root_v] = root_u
            else:
                self.parent[root_v] = root_u
                self.rank[root_u] += 1

def kruskal_mst(edges: List[Edge], V: int) -> List[Edge]:
    mst = []  # Resulting MST edges
    disjoint_set = DisjointSet(V)

    # Sort edges by weight
    edges.sort()

    for edge in edges:
        u = edge.src
        v = edge.dest

        # Check if the current edge forms a cycle
        if disjoint_set.find(u) != disjoint_set.find(v):
            mst.append(edge)
            disjoint_set.union(u, v)

    return mst

if __name__ == "__main__":
    V = 4  # Number of vertices
    edges = [
        Edge(0, 1, 1),
        Edge(0, 2, 3),
        Edge(1, 2, 3),
        Edge(1, 3, 6),
        Edge(2, 3, 4),
    ]

    mst = kruskal_mst(edges, V)

    print("Edges in the Minimum Spanning Tree:")
    for edge in mst:
        print(f"{edge.src} - {edge.dest} : {edge.weight}")

```

## Prim's Algorithm:

Start with an arbitrary vertex and grow the MST one edge at a time.
At each step, add the smallest edge that connects a vertex in the MST to a vertex outside the MST.
Repeat until all vertices are included in the MST.

### Workflow of Prim's Algorithm:
- Initialization:
  - Start with a single vertex (arbitrary choice).
  - Maintain a list of edges that connect vertices inside the MST to those outside.
  - Use a priority queue (min-heap) to efficiently get the smallest edge connecting the MST to the rest of the graph.

- Algorithm Execution:
  - Initialize all vertices as not being part of the MST.
  - Select the initial vertex and mark it as part of the MST.
  - Add all edges from this vertex to the priority queue.
  - While there are vertices not in the MST:
    - Extract the smallest edge from the priority queue.
    - If the destination vertex of this edge is not yet in the MST:
      - Add this edge to the MST.
      - Mark the destination vertex as part of the MST.
      - Add all edges from this new vertex to the priority queue.

- Result:

  The edges added during the iteration form the MST

### Implementation
```python
import heapq
from typing import List, Tuple

Edge = Tuple[int, int]  # First: weight, Second: destination vertex

def prim_mst(graph: List[List[Edge]], V: int) -> List[Edge]:
    mst = []  # Resulting MST edges
    in_mst = [False] * V  # Track vertices included in MST
    pq = []  # Min-heap priority queue

    # Start with the first vertex (0)
    in_mst[0] = True
    for edge in graph[0]:
        heapq.heappush(pq, edge)

    while pq:
        weight, v = heapq.heappop(pq)

        if in_mst[v]:
            continue

        in_mst[v] = True
        mst.append((weight, v))

        for next_edge in graph[v]:
            if not in_mst[next_edge[1]]:
                heapq.heappush(pq, next_edge)

    return mst

if __name__ == "__main__":
    V = 4  # Number of vertices
    graph = [[] for _ in range(V)]

    # Add edges to the graph
    graph[0].append((1, 1))
    graph[0].append((3, 2))
    graph[1].append((1, 0))
    graph[1].append((3, 2))
    graph[1].append((6, 3))
    graph[2].append((3, 0))
    graph[2].append((3, 1))
    graph[2].append((4, 3))
    graph[3].append((6, 1))
    graph[3].append((4, 2))

    mst = prim_mst(graph, V)

    print("Edges in the Minimum Spanning Tree:")
    for weight, vertex in mst:
        print(f"Vertex {vertex} with weight {weight}")
```

## Prim's Algorithm VS. Kruskal's Algorithm

Prim's algorithm and Kruskal's algorithm are both greedy algorithms used to solve the Minimum Spanning Tree (MST) problem, but they differ in their approach:

- **Choice of starting vertex**
  - Prim's algorithm starts with an arbitrary vertex and grows the MST from that vertex.
  - Kruskal's algorithm does not require a specific starting vertex; it processes all edges in the graph.

- **Edge selection**
  - Prim's algorithm selects the edge with the minimum weight that connects to the current node (i.e., the edge with the smallest weight that has one endpoint in the MST and the other endpoint outside the MST).
  - Kruskal's algorithm selects the edge with the minimum weight from all edges in the graph.

- **Union operation**
  - Prim's algorithm performs a union operation on the nodes connected by the selected edge, effectively merging two sets into one.
  - Kruskal's algorithm also performs a union operation, but it does so for each connected component (i.e., each set of nodes that is not yet part of the MST).

- **Time complexity**
  - Prim's algorithm has a time complexity of **O(E + V)**, where E is the number of edges and V is the number of vertices.
  - Kruskal's algorithm has a time complexity of **O(E log E)**, which is generally faster for large graphs.

- **Space complexity**
  - Both algorithms have a space complexity of O(V), as they need to store information about each vertex (i.e., its parent in the MST).

In summary, Prim's algorithm starts with an arbitrary vertex, grows the MST from that vertex, and selects edges based on their weight, while Kruskal's algorithm processes all edges in the graph, selects edges based on their weight, and performs union operations for each connected component.

## Leetcode Questions

| # | Problem | Difficulty |
|---|---------|------------|
| 1168 | [Optimize Water Distribution in a Village](../../leetcode_questions/1168_optimize_water_distribution_in_a_village.md) | Hard |
| 1135 | [Connecting Cities With Minimum Cost](../../leetcode_questions/1135_connecting_cities_with_minimum_cost.md) | Medium |
| 1584 | [Min Cost to Connect All Points](../../leetcode_questions/1584_min_cost_to_connect_all_points.md) | Medium |
| 1489 | [Find Critical and Pseudo-Critical Edges in Minimum Spanning Tree](../../leetcode_questions/1489_find_critical_and_pseudo_critical_edges_in_minimum_spanning_tree.md) | Hard |
