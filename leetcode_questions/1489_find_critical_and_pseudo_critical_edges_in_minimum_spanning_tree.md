# 1489. Find Critical and Pseudo-Critical Edges in Minimum Spanning Tree

**Difficulty:** 🔴 Hard

## Question link
(https://leetcode.com/problems/find-critical-and-pseudo-critical-edges-in-minimum-spanning-tree/)

## Question Description
Given a weighted undirected connected graph with n vertices numbered from 0 to n - 1, and an array edges where edges[i] = [ai, bi, weighti] represents a bidirectional and weighted edge between nodes ai and bi. A minimum spanning tree (MST) is a subset of the graph's edges that connects all vertices without cycles and with the minimum possible total edge weight.

Find all the critical and pseudo-critical edges in the given graph's minimum spanning tree (MST). An MST edge whose deletion from the graph would cause the MST weight to increase is called a critical edge. On the other hand, a pseudo-critical edge is that which can appear in some MSTs but not all.

Note that you can return the indices of the edges in any order.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/06/04/ex1.png" width="400" />
>
> Input: n = 5, edges = [[0,1,1],[1,2,1],[2,3,2],[0,3,2],[0,4,3],[3,4,3],[1,4,6]]
>
> Output: [[0,1],[2,3,4,5]]
>
> Explanation: The figure above describes the graph.
>
> The following figure shows all the possible MSTs:
>
> <img src="https://assets.leetcode.com/uploads/2020/06/04/msts.png" width="400" />
>
> Notice that the two edges 0 and 1 appear in all MSTs, therefore they are critical edges, so we return them in the first list of the output.
>
> The edges 2, 3, 4, and 5 are only part of some MSTs, therefore they are considered pseudo-critical edges. We add them to the second list of the output.

Example 2:
> <img src="https://assets.leetcode.com/uploads/2020/06/04/ex2.png" width="400" />
>
> Input: n = 4, edges = [[0,1,1],[1,2,1],[2,3,1],[0,3,1]]
>
> Output: [[],[0,1,2,3]]
>
> Explanation: We can observe that since all 4 edges have equal weight, choosing any 3 edges from the given 4 will yield an MST. Therefore all 4 edges are pseudo-critical.

<br/>

Constraints:
- 2 <= n <= 100
- 1 <= edges.length <= min(200, n * (n - 1) / 2)
- edges[i].length == 3
- 0 <= ai < bi < n
- 1 <= weighti <= 1000
- All pairs (ai, bi) are distinct.

## Tags
- graph
- mst

## Approach
**Key idea:** An edge is critical if removing it makes the MST heavier (or disconnects the graph). A non-critical edge is pseudo-critical if forcing it into the tree still gives the same MST weight.

1. Tag each edge with its original index and sort the edges by weight for Kruskal's algorithm.
2. Run Kruskal once to get the base MST weight.
3. For each edge, rerun Kruskal without it; if the graph can't be connected or the weight goes up, the edge is critical.
4. Otherwise, rerun Kruskal with that edge added first; if the weight still equals the base, the edge is pseudo-critical.
5. Return `[critical, pseudo_critical]`.

## Code Implementation
```python
class Solution:
    def findCriticalAndPseudoCriticalEdges(self, n: int, edges: list[list[int]]) -> list[list[int]]:
        # (weight, a, b, original index), sorted by weight for Kruskal
        indexed = sorted((w, a, b, i) for i, (a, b, w) in enumerate(edges))

        def mst(skip: int = -1, force: int = -1) -> int:
            """Kruskal MST weight, skipping / forcing an edge (by sorted position); -1 if disconnected."""
            parent = list(range(n))

            def find(x: int) -> int:
                while parent[x] != x:
                    parent[x] = parent[parent[x]]  # path halving
                    x = parent[x]
                return x

            total, components = 0, n
            if force != -1:
                w, a, b, _ = indexed[force]
                parent[find(a)] = find(b)
                total += w
                components -= 1
            for j, (w, a, b, _) in enumerate(indexed):
                if j == skip or j == force:
                    continue
                ra, rb = find(a), find(b)
                if ra != rb:
                    parent[ra] = rb
                    total += w
                    components -= 1
            return total if components == 1 else -1

        base = mst()
        critical, pseudo = [], []
        for j, (_, _, _, idx) in enumerate(indexed):
            without = mst(skip=j)
            if without == -1 or without > base:
                critical.append(idx)  # every MST needs this edge
            elif mst(force=j) == base:
                pseudo.append(idx)    # some MSTs use it, but not all
        return [critical, pseudo]
```

## Time Complexity Analysis
> Time complexity  : O(E log E + E^2 · α(V)) — one sort, then up to two Kruskal passes of O(E · α(V)) for each of the E edges
>
> Space complexity : O(V + E) — the sorted edge list and the union-find array

## Related Problems
- [1135. Connecting Cities With Minimum Cost](./1135_connecting_cities_with_minimum_cost.md) — 🟡 Medium · the basic Kruskal / Prim MST
- [1584. Min Cost to Connect All Points](./1584_min_cost_to_connect_all_points.md) — 🟡 Medium · MST on a complete graph
- [1192. Critical Connections in a Network](./1192_critical_connections_in_a_network.md) — 🔴 Hard · finds edges whose removal disconnects the graph
