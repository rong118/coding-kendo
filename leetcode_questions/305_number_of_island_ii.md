# 305. Number of Islands II

**Difficulty:** 🔴 Hard

## Question link
(https://leetcode.com/problems/number-of-islands-ii/)

## Question Description
A 2d grid map ofmrows andncolumns is initially filled with water. We may perform anaddLandoperation which turns the water at position (row, col) into a land. Given a list of positions to operate,count the number of islands after each addLand operation. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:
> Input: m = 3, n = 3, positions = [[0,0], [0,1], [1,2], [2,1]]
>
> Output: [1,1,2,3]
>
> Explanation: Initially, the 2d gridgridis filled with water. (Assume 0 represents water and 1 represents land).
>

Follow up:
- Can you do it in time complexity O(k log mn), where k is the length of thepositions?

## Tags
- dfs
- unionfind

## Approach
**Key idea:** Treat each land cell as a Union-Find node; adding land creates a new island, and every successful union with a neighboring island merges two islands into one.

1. Map cell `(x, y)` to id `x * n + y` and initialize a Union-Find over all `m * n` cells.
2. For each position: if it is already land, the count is unchanged — record it and continue.
3. Otherwise mark it as land and increment `count`.
4. For each of the 4 land neighbors, if its root differs from the new cell's root, union them and decrement `count`.
5. Append `count` after processing each position.

## Code Implementation
```python
class Solution:
    def numIslands2(self, m: int, n: int, positions: list[list[int]]) -> list[int]:
        parent = list(range(m * n))

        def find(x: int) -> int:
            while parent[x] != x:
                parent[x] = parent[parent[x]]  # path compression (halving)
                x = parent[x]
            return x

        land = [[False] * n for _ in range(m)]
        ans = []
        count = 0
        for x, y in positions:
            if land[x][y]:
                ans.append(count)
                continue
            land[x][y] = True
            count += 1
            for dx, dy in ((-1, 0), (1, 0), (0, -1), (0, 1)):
                nx, ny = x + dx, y + dy
                if 0 <= nx < m and 0 <= ny < n and land[nx][ny]:
                    r1, r2 = find(nx * n + ny), find(x * n + y)
                    if r1 != r2:
                        parent[r2] = r1
                        count -= 1
            ans.append(count)
        return ans
```

## Time Complexity Analysis
> Time complexity  : O(m * n + k * α(m * n)) — initializing the DSU plus near-constant work per position
>
> Space complexity : O(m * n) — parent array and land grid

## Related Problems
- [200. Number of Islands](https://leetcode.com/problems/number-of-islands) — 🟡 Medium · static version solved with DFS/BFS
- [547. Number of Provinces](./547_number_of_provinces.md) — 🟡 Medium · counting components with Union-Find
- [261. Graph Valid Tree](./261_graph_valid_tree.md) — 🟡 Medium · Union-Find merge detection
