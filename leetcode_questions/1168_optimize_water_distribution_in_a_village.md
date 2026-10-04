# 1168. Optimize Water Distribution in a Village

**Difficulty:** 🔴 Hard

## Question link
> (https://leetcode.com/problems/optimize-water-distribution-in-a-village/)

## Question Description
There are n houses in a village. We want to supply water for all the houses by building wells and laying pipes.

For each house i, we can either build a well inside it directly with cost wells[i], or pipe in water from another well to it. The costs to lay pipes between houses are given by the array pipes, where each pipes[i] = [house1, house2, cost] represents the cost to connect house1 and house2 together using a pipe. Connections are bidirectional.

Find the minimum total cost to supply water to all houses.

Example 1:
> <img src="https://camo.githubusercontent.com/2ede13124d2b65792127b24b9772f16378198a3a58ee5e62b242e4fcafaac53a/68747470733a2f2f747661312e73696e61696d672e636e2f6c617267652f30303753385a496c6c793167686c74796d6f6370676a33306369306263337a302e6a7067" width="400" />
>
> Input: n = 3, wells = [1,2,2], pipes = [[1,2,1],[2,3,1]]
> 
> Output: 3

> Explanation: 
> The image shows the costs of connecting houses using pipes.
> The best strategy is to build a well in the first house with cost 1 and connect the other houses to it with cost 2 so the total cost is 3.

Constraints:
- 1 <= n <= 10000
- wells.length == n
- 0 <= wells[i] <= 10^<sup>5</sup> 
- 1 <= pipes.length <= 10000
- 1 <= pipes[i][0], pipes[i][1] <= n
- 0 <= pipes[i][2] <= 10^<sup>5</sup> 
- pipes[i][0] != pipes[i][1]

<br/>

## Tags
- graph
- mst

## Approach
**Key idea:** Add a virtual node 0 for the water source and model building a well at house `i` as an edge `(0, i)` with cost `wells[i-1]`. The answer is then the minimum spanning tree of this `n + 1`-node graph.

1. Build an adjacency list: edges from node 0 to every house with the well cost, plus both directions of every pipe.
2. Run Prim's algorithm from node 0 with a min-heap of `(cost, node)`.
3. Pop the cheapest edge; skip it if the node is already in the tree, otherwise add the node and its cost to the total.
4. Push all edges from the new node to unvisited neighbors.
5. Stop once all `n + 1` nodes are in the tree and return the total.

## Code Implementation
```python
import heapq

class Solution:
    def minCostToSupplyWater(self, n: int, wells: list[int], pipes: list[list[int]]) -> int:
        # Virtual node 0 is the water source: building a well at house i = edge (0, i)
        graph = [[] for _ in range(n + 1)]
        for i, cost in enumerate(wells, start=1):
            graph[0].append((cost, i))
        for u, v, cost in pipes:
            graph[u].append((cost, v))
            graph[v].append((cost, u))

        visited = set()
        heap = [(0, 0)]
        total = 0
        while heap and len(visited) < n + 1:
            cost, node = heapq.heappop(heap)
            if node in visited:
                continue
            visited.add(node)
            total += cost
            for edge in graph[node]:
                if edge[1] not in visited:
                    heapq.heappush(heap, edge)
        return total
```

## Time Complexity Analysis
> Time complexity  : O((n + m) log(n + m)) — Prim with a heap, m = pipes.length
>
> Space complexity : O(n + m) — adjacency list and heap

## Related Problems
- [1135. Connecting Cities With Minimum Cost](./1135_connecting_cities_with_minimum_cost.md) — 🟡 Medium · plain MST over given edges
- [1584. Min Cost to Connect All Points](./1584_min_cost_to_connect_all_points.md) — 🟡 Medium · MST on a complete graph with Prim's
- [1489. Find Critical and Pseudo-Critical Edges in Minimum Spanning Tree](./1489_find_critical_and_pseudo_critical_edges_in_minimum_spanning_tree.md) — 🔴 Hard · MST edge analysis
