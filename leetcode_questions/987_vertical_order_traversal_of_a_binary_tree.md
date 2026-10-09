# 987. Vertical Order Traversal of a Binary Tree

**Difficulty:** 🔴 Hard

## Question link
(https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/)

## Question Description
Given the root of a binary tree, calculate the vertical order traversal of the binary tree.

For each node at position (row, col), its left and right children will be at positions (row + 1, col - 1) and (row + 1, col + 1) respectively. The root of the tree is at (0, 0).

The vertical order traversal of a binary tree is a list of top-to-bottom orderings for each column index starting from the leftmost column and ending on the rightmost column. There may be multiple nodes in the same row and same column. In such a case, sort these nodes by their values.

Return the vertical order traversal of the binary tree.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/01/29/vtree1.jpg" width="300" />
>
> Input: root = [3,9,20,null,null,15,7]
>
> Output: [[9],[3,15],[20],[7]]
>
> Explanation:
>
> Column -1: Only node 9 is in this column.
>
> Column 0: Nodes 3 and 15 are in this column in that order from top to bottom.
>
> Column 1: Only node 20 is in this column.
>
> Column 2: Only node 7 is in this column.

Example 2:
> <img src="https://assets.leetcode.com/uploads/2021/01/29/vtree2.jpg" width="300" />
>
> Input: root = [1,2,3,4,5,6,7]
>
> Output: [[4],[2],[1,5,6],[3],[7]]
>
> Explanation:
>
> Column -2: Only node 4 is in this column.
>
> Column -1: Only node 2 is in this column.
>
> Column 0: Nodes 1, 5, and 6 are in this column.
>
>         1 is at the top, so it comes first.
>
>         5 and 6 are at the same position (2, 0), so we order them by their value, 5 before 6.
>
> Column 1: Only node 3 is in this column.
>
> Column 2: Only node 7 is in this column.

Example 3:
><img src="https://assets.leetcode.com/uploads/2021/01/29/vtree3.jpg" width="300" />
>
> Input: root = [1,2,3,4,6,5,7]
>
> Output: [[4],[2],[1,5,6],[3],[7]]
>
> Explanation:
>
> This case is the exact same as example 2, but with nodes 5 and 6 swapped.
>
> Note that the solution remains the same since 5 and 6 are in the same location and should be ordered by their values.
 
Constraints:
- The number of nodes in the tree is in the range [1, 1000].
- 0 <= Node.val <= 1000

## Tags
- tree

## Approach
**Key idea:** Record every node's `(row, col)` position with a DFS, group nodes by column, then sort each column by `(row, value)` — that ordering is exactly "top to bottom, ties broken by value".

1. DFS from the root at `(row 0, col 0)`; a left child goes to `(row + 1, col - 1)`, a right child to `(row + 1, col + 1)`.
2. Append `(row, val)` to the list for the node's column.
3. Visit the columns from smallest to largest.
4. Sort each column's `(row, val)` pairs and output just the values.

## Code Implementation
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import defaultdict

class Solution:
    def verticalTraversal(self, root: Optional[TreeNode]) -> list[list[int]]:
        cols = defaultdict(list)  # col -> [(row, val), ...]

        def dfs(node: Optional[TreeNode], row: int, col: int) -> None:
            if not node:
                return
            cols[col].append((row, node.val))
            dfs(node.left, row + 1, col - 1)
            dfs(node.right, row + 1, col + 1)

        dfs(root, 0, 0)
        return [[val for _, val in sorted(cols[c])] for c in sorted(cols)]
```

## Time Complexity Analysis
> Time complexity  : O(n log n) — sorting the nodes within columns (and the columns themselves)
>
> Space complexity : O(n)

## Related Problems
- [314. Binary Tree Vertical Order Traversal](./314_binary_tree_vertical_order_traversal.md) — 🟡 Medium · same column grouping, ties broken by BFS order instead of value
- [102. Binary Tree Level Order Traversal](./102_binary_tree_level_order_traversal.md) — 🟡 Medium · grouping nodes by row instead of column
- [103. Binary Tree Zigzag Level Order Traversal](./103_binary_tree_zigzig_level_order_traversal.md) — 🟡 Medium · grouping nodes by level with ordering rules
