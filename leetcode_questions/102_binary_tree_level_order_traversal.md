# 102. Binary Tree Level Order Traversal

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/binary-tree-level-order-traversal/)

## Question Description
Given the root of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg" width="300" />
> 
> Input: root = [3,9,20,null,null,15,7]
>
> Output: [[3],[9,20],[15,7]]

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
**Key idea:** BFS visits nodes in exactly level order; processing the queue one level at a time (using its current size) groups the values by depth.

1. If `root` is empty, return `[]`; otherwise push `root` into a queue.
2. While the queue is non-empty, record its current size — that is the number of nodes on this level.
3. Pop that many nodes, append their values to a `level` list, and push their non-null children.
4. Append `level` to the answer and continue with the next level.
5. Alternative (DFS): recurse with a `depth` argument and append each value to `ans[depth]`, creating the list the first time a depth is reached.

## Code Implementation
### Approach 1: BFS
```python
from collections import deque
from typing import Optional

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> list[list[int]]:
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
        return ans
```

### Approach 2: DFS (recursive)
```python
from typing import Optional

class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> list[list[int]]:
        ans = []

        def dfs(node: Optional[TreeNode], depth: int) -> None:
            if not node:
                return
            if depth == len(ans):
                ans.append([])
            ans[depth].append(node.val)
            dfs(node.left, depth + 1)
            dfs(node.right, depth + 1)

        dfs(root, 0)
        return ans
```

## Time Complexity Analysis
> Time complexity  : O(n) — every node is visited once (both approaches)
>
> Space complexity : O(n) — BFS queue holds up to a full level (~n/2 nodes); DFS uses O(h) recursion stack, plus O(n) for the output

## Related Problems
- [107. Binary Tree Level Order Traversal II](./107_binary_tree_level_order_traversal_II.md) — 🟡 Medium · same BFS, levels returned bottom-up
- [103. Binary Tree Zigzag Level Order Traversal](./103_binary_tree_zigzig_level_order_traversal.md) — 🟡 Medium · level order with alternating direction
- [199. Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view) — 🟡 Medium · last node of each BFS level
- [314. Binary Tree Vertical Order Traversal](./314_binary_tree_vertical_order_traversal.md) — 🟡 Medium · BFS grouped by column instead of depth
