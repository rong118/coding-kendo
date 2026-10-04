# 95. Unique Binary Search Trees II

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/unique-binary-search-trees-ii/)

## Question Description
Given an integer n, return all the structurally unique BST's (binary search trees), which has exactly n nodes of unique values from 1 to n. Return the answer in any order.

<br/>

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg" width="400" />
>
> Input: n = 3
> 
> Output: [[1,null,2,null,3],[1,null,3,2],[2,1,3],[3,1,null,null,2],[3,2,null,1]]

Example 2:
> Input: n = 1
>
> Output: [[1]]

Constraints:
- 1 <= n <= 8

## Tags
- tree
- dfs

## Approach
**Key idea:** Picking `i` as the root of a BST on `[start, end]` forces `[start, i - 1]` into the left subtree and `[i + 1, end]` into the right, so every tree is a root combined with any left subtree and any right subtree built recursively.

1. Define `build(start, end)` that returns every BST using values `start..end`.
2. If `start > end`, return `[None]` (the single empty tree).
3. For each root value `i` in the range, recursively build all left subtrees from `[start, i - 1]` and all right subtrees from `[i + 1, end]`.
4. For every (left, right) pair, create a new root `i` with those children and add it to the result.
5. Return `build(1, n)`.

## Code Implementation
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def generateTrees(self, n: int) -> list[Optional[TreeNode]]:
        def build(start: int, end: int) -> list[Optional[TreeNode]]:
            if start > end:
                return [None]

            trees = []
            for i in range(start, end + 1):
                lefts = build(start, i - 1)
                rights = build(i + 1, end)
                for left in lefts:
                    for right in rights:
                        trees.append(TreeNode(i, left, right))
            return trees

        return build(1, n)
```

## Time Complexity Analysis
> Time complexity  : O(n · G(n)) ≈ O(4^n / √n), where G(n) is the nth Catalan number (the number of unique BSTs)
>
> Space complexity : O(n · G(n)) ≈ O(4^n / √n) — G(n) trees of up to n nodes each

## Related Problems
- [96. Unique Binary Search Trees](./96_unique_binary_search_trees.md) — 🟡 Medium · count these trees instead of building them (Catalan DP)
- [108. Convert Sorted Array to Binary Search Tree](./108_convert_sorted_array_to_binary_search_tree.md) — 🟢 Easy · pick a root, recurse on left and right ranges
- [894. All Possible Full Binary Trees](https://leetcode.com/problems/all-possible-full-binary-trees) — 🟡 Medium · same combine-all-left-and-right-subtrees recursion
