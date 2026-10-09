# 96. Unique Binary Search Trees

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/unique-binary-search-trees/)

## Question Description
Given an integer n, return the number of structurally unique BST's (binary search trees) which has exactly n nodes of unique values from 1 to n.

<br/>

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg" width="400" />
>
> Input: n = 3
>
> Output: 5

Example 2:
>
>
> Input: n = 1
>
> Output: 1

Constraints:
- 1 <= n <= 19

## Tags
- tree
- dp

## Approach
**Key idea:** Pick each value `i` as the root: the left subtree is any BST of the `i - 1` smaller values and the right subtree is any BST of the `n - i` larger values, so `G(n) = sum(G(i - 1) * G(n - i))` for `i = 1..n` (the Catalan numbers).

1. Let `G(k)` be the number of unique BSTs with `k` nodes; `G(0) = G(1) = 1`.
2. For each root choice `i`, multiply the counts of possible left and right subtrees.
3. Sum over all roots to get `G(k)`.
4. Compute it top-down with memoization (Approach 1) or bottom-up for `k = 2..n` (Approach 2), and return `G(n)`.

## Code Implementation
### Approach 1: Memoized Recursion
```python
class Solution:
    def numTrees(self, n: int) -> int:
        memo = {0: 1, 1: 1}

        def count(k: int) -> int:
            if k in memo:
                return memo[k]
            memo[k] = sum(count(i - 1) * count(k - i) for i in range(1, k + 1))
            return memo[k]

        return count(n)
```

### Approach 2: Bottom-up DP
```python
class Solution:
    def numTrees(self, n: int) -> int:
        # g[k] = number of unique BSTs with k nodes
        g = [0] * (n + 1)
        g[0] = 1
        for i in range(1, n + 1):
            for j in range(1, i + 1):  # j is the root
                g[i] += g[j - 1] * g[i - j]
        return g[n]
```

## Time Complexity Analysis
> Time complexity  : O(n^2)
>
> Space complexity : O(n)

## Related Problems
- [95. Unique Binary Search Trees II](./95_unique_binary_search_trees_ii.md) — 🟡 Medium · same root-split recursion, but builds the actual trees
- [108. Convert Sorted Array to Binary Search Tree](./108_convert_sorted_array_to_binary_search_tree.md) — 🟢 Easy · choosing a root splits values into left/right subtrees
- [98. Validate Binary Search Tree](./98_validate_binary_search_tree.md) — 🟡 Medium · BST ordering property
