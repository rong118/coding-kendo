# 547 Number of Provinces

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/number-of-provinces/)

## Question Description
There are n cities. Some of them are connected, while some are not. If city a is connected directly with city b, and city b is connected directly with city c, then city a is connected indirectly with city c.
A province is a group of directly or indirectly connected cities and no other cities outside of the group.
You are given an n x n matrix isConnected where isConnected[i][j] = 1 if the i<sup>th</sup> city and the jth city are directly connected, and isConnected[i][j] = 0 otherwise.

Return the total number of provinces.

Example 1:
> ![Image](https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg)
>
> Input: isConnected = [[1,1,0],[1,1,0],[0,0,1]]
>
> Output: 2

Example 2:
> ![Image](https://assets.leetcode.com/uploads/2020/12/24/graph2.jpg)
>
> Input: isConnected = [[1,0,0],[0,1,0],[0,0,1]]
>
> Output: 3

Constraints:
- 1 <= n <= 200
- n == isConnected.length
- n == isConnected[i].length
- isConnected[i][j] is 1 or 0.
- isConnected[i][i] == 1
- isConnected[i][j] == isConnected[j][i]

## Tags
- graph
- unionfind

## Approach
**Key idea:** A province is a connected component, so union every directly connected pair in a disjoint-set union (DSU); the number of distinct roots left is the number of provinces.

1. Initialize a DSU where every city is its own parent.
2. For every pair `(i, j)` with `isConnected[i][j] == 1`, union `i` and `j`.
3. `find` uses path compression so later lookups are nearly constant time.
4. Count the cities that are their own root (`find(i) == i`) and return that count.

## Code Implementation
```python
class DSU:
    def __init__(self, n: int):
        self.parent = list(range(n))

    def find(self, x: int) -> int:
        while self.parent[x] != x:
            self.parent[x] = self.parent[self.parent[x]]  # path compression (halving)
            x = self.parent[x]
        return x

    def union(self, x: int, y: int) -> None:
        self.parent[self.find(x)] = self.find(y)


class Solution:
    def findCircleNum(self, isConnected: list[list[int]]) -> int:
        n = len(isConnected)
        dsu = DSU(n)
        for i in range(n):
            for j in range(n):
                if isConnected[i][j] == 1:
                    dsu.union(i, j)
        return sum(1 for i in range(n) if dsu.find(i) == i)
```

## Time Complexity Analysis
> Time complexity  : O(n² · log n) — n² cells, each possibly a union; path compression alone gives O(log n) amortized per operation (nearly O(n²) in practice)
>
> Space complexity : O(n) — the parent array

## Related Problems
- [261. Graph Valid Tree](./261_graph_valid_tree.md) — 🟡 Medium · union-find to detect cycles and count components
- [305. Number of Islands II](./305_number_of_island_ii.md) — 🔴 Hard · union-find counting components dynamically
- [200. Number of Islands](https://leetcode.com/problems/number-of-islands) — 🟡 Medium · counting connected components on a grid
- [1135. Connecting Cities With Minimum Cost](./1135_connecting_cities_with_minimum_cost.md) — 🟡 Medium · union-find inside Kruskal's MST
