# 1192. Critical Connections in a Network

**Difficulty:** 🔴 Hard

## Question link
> (https://leetcode.com/problems/critical-connections-in-a-network/)

## Question Description
There are n servers numbered from 0 to n - 1 connected by undirected server-to-server connections forming a network where connections[i] = [ai, bi] represents a connection between servers ai and bi. Any server can reach other servers directly or indirectly through the network.

A critical connection is a connection that, if removed, will make some servers unable to reach some other server.

Return all critical connections in the network in any order.

<br/>

Example 1:
>
> <img src="https://assets.leetcode.com/uploads/2019/09/03/1537_ex1_2.png" width="400" />
>
> Input: n = 4, connections = [[0,1],[1,2],[2,0],[1,3]]
>
> Output: [[1,3]]
>
> Explanation: [[3,1]] is also accepted.

Example 2:
>
> Input: n = 2, connections = [[0,1]]
>
> Output: [[0,1]]

Constraints:
- 2 <= n <= 10<sup>5</sup> 
- n - 1 <= connections.length <= 10<sup>5</sup>
- 0 <= ai, bi <= n - 1
- ai != bi
- There are no repeated connections.

## Tags
- graph
- tarjan

## Approach
**Key idea:** Tarjan's bridge-finding algorithm: in a DFS, an edge `cur -> nei` is a bridge exactly when nothing in `nei`'s subtree can reach `cur` or an earlier node without that edge, i.e. `low[nei] > dfn[cur]`.

1. Build an adjacency list from `connections`.
2. DFS from each unvisited node, stamping `dfn[cur]` (discovery time) and initializing `low[cur]` to the same value.
3. For each neighbor (skipping the edge back to the parent): if unvisited, recurse and pull `low[cur]` down to `low[nei]`; if already visited, it is a back edge, so pull `low[cur]` down to `dfn[nei]`.
4. After returning from a child `nei`, if `low[nei] > dfn[cur]`, record `[cur, nei]` as a critical connection.
5. Return all recorded edges.

## Code Implementation
```python
import sys

class Solution:
    def criticalConnections(self, n: int, connections: list[list[int]]) -> list[list[int]]:
        sys.setrecursionlimit(max(1000, 2 * n + 10))  # DFS depth can reach n

        graph = [[] for _ in range(n)]
        for a, b in connections:
            graph[a].append(b)
            graph[b].append(a)

        dfn = [-1] * n  # discovery time, -1 = unvisited
        low = [0] * n   # earliest discovery time reachable from the subtree
        res = []
        time = 0

        def dfs(cur: int, parent: int) -> None:
            nonlocal time
            time += 1
            dfn[cur] = low[cur] = time
            for nei in graph[cur]:
                if nei == parent:
                    continue
                if dfn[nei] == -1:
                    dfs(nei, cur)
                    low[cur] = min(low[cur], low[nei])
                    if low[nei] > dfn[cur]:
                        res.append([cur, nei])
                else:
                    low[cur] = min(low[cur], dfn[nei])

        for i in range(n):
            if dfn[i] == -1:
                dfs(i, -1)

        return res
```

## Time Complexity Analysis
> Time complexity  : O(V + E) — each node and edge is processed once in the DFS
>
> Space complexity : O(V + E) — adjacency list, `dfn`/`low` arrays and recursion stack

## Related Problems
- [1489. Find Critical and Pseudo-Critical Edges in Minimum Spanning Tree](./1489_find_critical_and_pseudo_critical_edges_in_minimum_spanning_tree.md) — 🔴 Hard · identifying edges whose removal changes the graph
- [261. Graph Valid Tree](./261_graph_valid_tree.md) — 🟡 Medium · connectivity and cycles in an undirected graph
- [547. Number of Provinces](./547_number_of_provinces.md) — 🟡 Medium · DFS over connected components
- [1568. Minimum Number of Days to Disconnect Island](https://leetcode.com/problems/minimum-number-of-days-to-disconnect-island) — 🔴 Hard · articulation points via Tarjan's low-link
