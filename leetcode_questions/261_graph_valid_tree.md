# 261 Graph Valid Tree

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/graph-valid-tree/description/)

## Question Description
Givennnodes labeled from0ton - 1and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree.

For example:
Givenn = 5andedges = [[0, 1], [0, 2], [0, 3], [1, 4]], return true.
Givenn = 5andedges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]], return false.

Note: you can assume that no duplicate edges will appear inedges. Since all edges are undirected,[0, 1]is the same as[1, 0]and thus will not appear together inedges.

## Tags
- graph
- dfs
- union find

## Approach
**Key idea:** A graph on `n` nodes is a tree exactly when it has `n - 1` edges and no cycle (equivalently, it is connected and acyclic).

1. If the number of edges is not `n - 1`, it cannot be a tree.
2. Union Find: for each edge, find the roots of both endpoints; if they already share a root, the edge closes a cycle.
3. Otherwise, union the two components and continue. With `n - 1` edges and no cycle, the graph is connected.
4. DFS: build an adjacency list and traverse from node 0, remembering each node's parent.
5. Reaching an already-visited node that is not the parent means a cycle; at the end every node must have been visited.

## Code Implementation
### Approach 1: Union Find
```python
class Solution:
    def validTree(self, n: int, edges: list[list[int]]) -> bool:
        if len(edges) != n - 1:
            return False

        parent = list(range(n))
        size = [1] * n

        def find(x: int) -> int:
            while parent[x] != x:
                parent[x] = parent[parent[x]]  # path halving
                x = parent[x]
            return x

        for a, b in edges:
            ra, rb = find(a), find(b)
            if ra == rb:
                return False  # edge closes a cycle
            if size[ra] < size[rb]:
                ra, rb = rb, ra
            parent[rb] = ra
            size[ra] += size[rb]
        return True
```

### Approach 2: DFS with parent
```python
class Solution:
    def validTree(self, n: int, edges: list[list[int]]) -> bool:
        graph = [[] for _ in range(n)]
        for a, b in edges:
            graph[a].append(b)
            graph[b].append(a)

        visited = [False] * n
        visited[0] = True
        stack = [(0, -1)]  # (node, parent)
        while stack:
            node, parent = stack.pop()
            for nei in graph[node]:
                if nei == parent:
                    continue
                if visited[nei]:
                    return False  # reached a visited non-parent node: cycle
                visited[nei] = True
                stack.append((nei, node))

        return all(visited)
```

## Time Complexity Analysis
> Time complexity  : O(n · α(n)) union find (≈ O(n)); O(n + e) DFS, where e is the number of edges
>
> Space complexity : O(n) union find; O(n + e) DFS (adjacency list)

## Related Problems
- [547. Number of Provinces](./547_number_of_provinces.md) — 🟡 Medium · connected components with union find / DFS
- [323. Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph) — 🟡 Medium · same union find setup
- [207. Course Schedule](./207_course_schedule.md) — 🟡 Medium · cycle detection in a (directed) graph
- [305. Number of Islands II](./305_number_of_island_ii.md) — 🔴 Hard · incremental union find
