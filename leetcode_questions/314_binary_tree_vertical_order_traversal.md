# 314. Binary Tree Vertical Order Traversal

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/binary-tree-vertical-order-traversal/)

## Question Description
Given a binary tree, return the vertical order traversal of its nodes' values. (ie, from top to bottom, column by column).

If two nodes are in the same row and column, the order should be from left to right.

Example 1:
> Input: [3,9,20,null,null,15,7],
> 
> Output: [
>  [9],
>  [3,15],
>  [20],
>  [7]
> ]

Example 2:
> Input: [3,9,8,4,0,1,7],
>
> Output: [
>  [4],
>  [9],
>  [3,0,1],
>  [8],
>  [7]
> ]

Example 3:
> Input: [3,9,8,4,0,1,7,null,null,null,2,5] (0's right child is 2 and 1's left child is 5),
>
> Output: [
>  [4],
>  [9,5],
>  [3,0,1],
>  [8,2],
>  [7]
> ]

## Tags
- tree
- treemap

## Approach
**Key idea:** Give the root column `0`, a left child `column - 1` and a right child `column + 1`; a BFS visits nodes top to bottom and left to right, so appending values per column in BFS order gives exactly the required ordering.

1. Return `[]` for an empty tree; otherwise start a queue with `(root, 0)`.
2. Pop a node, append its value to its column's list, and track the min and max column seen.
3. Enqueue the left child with `column - 1` and the right child with `column + 1`.
4. After the BFS, output the column lists from the min column to the max column.

> Note: sorting each column by `(depth, value)` would order same-row nodes by value — that is the rule of [987](./987_vertical_order_traversal_of_a_binary_tree.md). Problem 314 requires left-to-right order instead, which the BFS guarantees.

## Code Implementation
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import defaultdict, deque

class Solution:
    def verticalOrder(self, root: Optional[TreeNode]) -> list[list[int]]:
        if not root:
            return []

        columns = defaultdict(list)
        min_col = max_col = 0
        queue = deque([(root, 0)])
        while queue:
            node, col = queue.popleft()
            columns[col].append(node.val)
            min_col = min(min_col, col)
            max_col = max(max_col, col)
            if node.left:
                queue.append((node.left, col - 1))
            if node.right:
                queue.append((node.right, col + 1))

        return [columns[c] for c in range(min_col, max_col + 1)]
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node is visited once; tracking min/max column avoids sorting
>
> Space complexity : O(n) — the queue and the column map

## Related Problems
- [987. Vertical Order Traversal of a Binary Tree](./987_vertical_order_traversal_of_a_binary_tree.md) — 🔴 Hard · same columns, but ties broken by value
- [102. Binary Tree Level Order Traversal](./102_binary_tree_level_order_traversal.md) — 🟡 Medium · the underlying BFS
- [199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view) — 🟡 Medium · BFS with per-level position bookkeeping
