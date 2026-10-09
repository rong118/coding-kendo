# 1584. Min Cost to Connect All Points

**Difficulty:** 🟡 Medium

## Question link
> (https://leetcode.com/problems/min-cost-to-connect-all-points/)

## Question Description
You are given an array points representing integer coordinates of some points on a 2D-plane, where points[i] = [xi, yi].

The cost of connecting two points [xi, yi] and [xj, yj] is the manhattan distance between them: |xi - xj| + |yi - yj|, where |val| denotes the absolute value of val.

Return the minimum cost to make all points connected. All points are connected if there is exactly one simple path between any two points.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/08/26/d.png" width="400" />
>
> Input: points = [[0,0],[2,2],[3,10],[5,2],[7,0]]
> 
> Output: 20
> 
> Explanation:
> 
> <img src="https://assets.leetcode.com/uploads/2020/08/26/c.png" width="400" />
>
> We can connect the points as shown above to get the minimum cost of 20.
>
> Notice that there is a unique path between every pair of points.

Example 2:
> Input: points = [[3,12],[-2,5],[-4,1]]
>
> Output: 18
>

Constraints:
- 1 <= points.length <= 1000
- -10<sup>6</sup> <= xi, yi <= 10<sup>6</sup>
- All pairs (xi, yi) are distinct.

## Tags
- graph
- mst

## Approach
**Key idea:** The points form a complete graph weighted by Manhattan distance, and the answer is its minimum spanning tree. On a dense graph, array-based Prim's in O(n²) is the best fit and needs no heap.

1. Keep `dist[i]`, the cheapest edge from point `i` to the tree so far (`0` for the start point, infinity elsewhere).
2. Repeat `n` times: pick the unvisited point `u` with the smallest `dist`, mark it visited, and add `dist[u]` to the total.
3. For every unvisited point `v`, update `dist[v]` with the Manhattan distance from `u` if it is smaller.
4. Return the total cost.

## Code Implementation
```python
class Solution:
    def minCostConnectPoints(self, points: list[list[int]]) -> int:
        n = len(points)
        dist = [float('inf')] * n
        dist[0] = 0
        visited = [False] * n
        total = 0
        for _ in range(n):
            # Pick the closest point not yet in the tree
            u = min((j for j in range(n) if not visited[j]), key=dist.__getitem__)
            visited[u] = True
            total += dist[u]
            ux, uy = points[u]
            for v in range(n):
                if not visited[v]:
                    d = abs(ux - points[v][0]) + abs(uy - points[v][1])
                    if d < dist[v]:
                        dist[v] = d
        return total
```

## Time Complexity Analysis
> Time complexity  : O(n²) — n rounds, each scanning all points
>
> Space complexity : O(n) — distance and visited arrays (distances computed on the fly)

## Related Problems
- [1135. Connecting Cities With Minimum Cost](./1135_connecting_cities_with_minimum_cost.md) — 🟡 Medium · MST over a sparse edge list
- [1168. Optimize Water Distribution in a Village](./1168_optimize_water_distribution_in_a_village.md) — 🔴 Hard · MST with a virtual source node
- [1489. Find Critical and Pseudo-Critical Edges in Minimum Spanning Tree](./1489_find_critical_and_pseudo_critical_edges_in_minimum_spanning_tree.md) — 🔴 Hard · MST edge analysis
