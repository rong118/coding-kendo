# 103. Binary Tree Zigzag Level Order Traversal

**Difficulty:** 🟡 Medium

## Question link
> link

## Question Description
Given the root of a binary tree, return the zigzag level order traversal of its nodes' values. (i.e., from left to right, then right to left for the next level and alternate between).

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg" width="400" />
>
> Input: root = [3,9,20,null,null,15,7]
>
> Output: [[3],[20,9],[15,7]]

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
- -100 <= Node.val <= 100

## Tags
- tree
- bfs

## Approach
**Key idea:** This is a normal level-order traversal; the only twist is that every odd level is read right to left.

1. BFS: put the root in a queue and process the tree one level at a time (the queue size tells you how many nodes are on the level).
2. Collect the level's values left to right while pushing each node's children.
3. Reverse the level if its index is odd, then add it to the answer.
4. DFS alternative: pass the depth down; on even depths append the value, on odd depths prepend it.

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
    def zigzagLevelOrder(self, root: Optional[TreeNode]) -> list[list[int]]:
        if not root:
            return []
        ans = []
        q = deque([root])
        while q:
            level = []
            for _ in range(len(q)):
                node = q.popleft()
                level.append(node.val)
                if node.left:
                    q.append(node.left)
                if node.right:
                    q.append(node.right)
            if len(ans) % 2 == 1:
                level.reverse()
            ans.append(level)
        return ans
```

### Approach 2: DFS (recursive)

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
    def zigzagLevelOrder(self, root: Optional[TreeNode]) -> list[list[int]]:
        ans: list[deque[int]] = []

        def dfs(node: Optional[TreeNode], depth: int) -> None:
            if not node:
                return
            if depth == len(ans):
                ans.append(deque())
            if depth % 2 == 0:
                ans[depth].append(node.val)
            else:
                ans[depth].appendleft(node.val)
            dfs(node.left, depth + 1)
            dfs(node.right, depth + 1)

        dfs(root, 0)
        return [list(level) for level in ans]
```

## Time Complexity Analysis
> Time complexity  : O(n) — every node is visited once
>
> Space complexity : O(n) — the queue holds up to one full level (BFS); recursion stack O(h) plus the output (DFS)

## Related Problems
- [102. Binary Tree Level Order Traversal](./102_binary_tree_level_order_traversal.md) — 🟡 Medium · the same BFS without the zigzag
- [107. Binary Tree Level Order Traversal II](./107_binary_tree_level_order_traversal_II.md) — 🟡 Medium · level order, bottom-up
- [314. Binary Tree Vertical Order Traversal](./314_binary_tree_vertical_order_traversal.md) — 🟡 Medium · BFS that groups nodes by column
