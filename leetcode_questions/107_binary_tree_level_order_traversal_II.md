# 107. Binary Tree Level Order Traversal II

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/binary-tree-level-order-traversal-ii/)

## Question Description
Given the root of a binary tree, return the bottom-up level order traversal of its nodes' values. (i.e., from left to right, level by level from leaf to root).

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg" width="400" />
>
> Input: root = [3,9,20,null,null,15,7]
> 
> Output: [[15,7],[9,20],[3]]

Example 2:
> Input: root = [1]
>
> Output: [[1]]

Example 3:
> Input: root = []
>
> Output: []

Constraints:
- The number of nodes in the tree is in the range [0, 2000].
- -1000 <= Node.val <= 1000

## Tags
- tree
- bfs

## Approach
**Key idea:** A bottom-up level order is just a normal top-down BFS level order, reversed at the end.

1. Return `[]` for an empty tree; otherwise start a queue with the root.
2. While the queue is non-empty, pop exactly the number of nodes currently in it — that is one level.
3. Record each popped node's value and enqueue its non-null children.
4. Append the level's values to the answer.
5. Reverse the answer so the deepest level comes first.

## Code Implementation
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque

class Solution:
    def levelOrderBottom(self, root: Optional[TreeNode]) -> list[list[int]]:
        if not root:
            return []

        ans = []
        queue = deque([root])
        while queue:
            level = []
            for _ in range(len(queue)):
                node = queue.popleft()
                level.append(node.val)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
            ans.append(level)

        return ans[::-1]
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node is enqueued and dequeued once
>
> Space complexity : O(n) — the queue and the output

## Related Problems
- [102. Binary Tree Level Order Traversal](./102_binary_tree_level_order_traversal.md) — 🟡 Medium · the same BFS without the final reverse
- [103. Binary Tree Zigzag Level Order Traversal](./103_binary_tree_zigzig_level_order_traversal.md) — 🟡 Medium · level-order BFS with alternating direction
- [637. Average of Levels in Binary Tree](https://leetcode.com/problems/average-of-levels-in-binary-tree) — 🟢 Easy · per-level BFS aggregation
