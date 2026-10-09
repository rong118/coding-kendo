# 1135. Connecting Cities With Minimum Cost

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/connecting-cities-with-minimum-cost/)

## Question Description
There are N cities numbered from 1 to N.

You are given connections, where each connections[i] = [city1, city2, cost] represents the cost to connect city1 and city2 together.  (A connection is bidirectional: connecting city1 and city2 is the same as connecting city2 and city1.)

Return the minimum cost so that for every pair of cities, there exists a path of connections (possibly of length 1) that connects those two cities together.  The cost is the sum of the connection costs used. If the task is impossible, return -1.

Example 1:

> Input: N = 3, connections = [[1,2,5],[1,3,6],[2,3,1]]
>
> Output: 6
>
> Explanation: 
>
> Choosing any 2 edges will connect all cities so we choose the minimum 2.

Example 2:

> Input: N = 4, connections = [[1,2,3],[3,4,4]]
>
> Output: -1
>
> Explanation: 
>
> There is no way to connect all cities even if all edges are used.
 

Note:
- 1 <= N <= 10000
- 1 <= connections.length <= 10000
- 1 <= connections[i][0], connections[i][1] <= N
- 0 <= connections[i][2] <= 10^5
- connections[i][0] != connections[i][1]

<br/>

## Tags
- graph 
- mst

## Approach
**Key idea:** The cheapest way to connect every city is a minimum spanning tree (MST). Prim's algorithm grows the tree from one city by always taking the cheapest edge out of it; Kruskal's algorithm adds the cheapest edges overall, skipping any edge that would form a cycle.

1. Prim: build an adjacency list and push `(0, city 1)` onto a min-heap.
2. Pop the cheapest entry; skip it if the city is already in the tree, otherwise add the city and its cost, and push its edges to cities not yet in the tree.
3. Kruskal: sort the edges by cost and use union-find; take an edge only if its endpoints are in different components, then merge them.
4. If not every city ends up connected (fewer than `n` visited, or more than one component left), return `-1`.

## Code Implementation
### Approach 1: Prim's algorithm

```python
import heapq
from collections import defaultdict


class Solution:
    def minimumCost(self, n: int, connections: list[list[int]]) -> int:
        graph = defaultdict(list)
        for x, y, cost in connections:
            graph[x].append((cost, y))
            graph[y].append((cost, x))

        visited = set()
        total = 0
        heap = [(0, 1)]  # (cost to reach city, city)
        while heap and len(visited) < n:
            cost, city = heapq.heappop(heap)
            if city in visited:
                continue
            visited.add(city)
            total += cost
            for edge in graph[city]:
                if edge[1] not in visited:
                    heapq.heappush(heap, edge)

        return total if len(visited) == n else -1
```

### Approach 2: Kruskal's algorithm

```python
class Solution:
    def minimumCost(self, n: int, connections: list[list[int]]) -> int:
        parent = list(range(n + 1))

        def find(x: int) -> int:
            while parent[x] != x:
                parent[x] = parent[parent[x]]  # path halving
                x = parent[x]
            return x

        total = 0
        components = n
        for x, y, cost in sorted(connections, key=lambda c: c[2]):
            rx, ry = find(x), find(y)
            if rx != ry:
                parent[rx] = ry
                total += cost
                components -= 1

        return total if components == 1 else -1
```

## Time Complexity Analysis
> Time complexity  : O(E log E) — the heap operations (Prim) or the edge sort (Kruskal) dominate; E log E = O(E log V)
>
> Space complexity : O(V + E) — adjacency list and heap (Prim); O(V) union-find plus the sorted edge copy (Kruskal)

## Related Problems
- [1584. Min Cost to Connect All Points](./1584_min_cost_to_connect_all_points.md) — 🟡 Medium · MST on a complete graph of points
- [1168. Optimize Water Distribution in a Village](./1168_optimize_water_distribution_in_a_village.md) — 🔴 Hard · MST with a virtual source node
- [1489. Find Critical and Pseudo-Critical Edges in Minimum Spanning Tree](./1489_find_critical_and_pseudo_critical_edges_in_minimum_spanning_tree.md) — 🔴 Hard · reruns Kruskal to classify edges
