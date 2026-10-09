# 257. Binary Tree Paths

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/binary-tree-paths/)

## Question Description
Given the root of a binary tree, return all root-to-leaf paths in any order.

A leaf is a node with no children.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/03/12/paths-tree.jpg" width="400" />
>
> Input: root = [1,2,3,null,5]
>
> Output: ["1->2->5","1->3"]

Example 2:
>
> Input: root = [1]
>
> Output: ["1"]

<br/>

Constraints:
- The number of nodes in the tree is in the range [1, 100].
- -100 <= Node.val <= 100

## Tags
- tree
- dfs

## Approach
**Key idea:** DFS from the root while carrying the path string built so far; a path is complete exactly when you reach a leaf.

1. Start a DFS at the root with an empty path.
2. At each node, append `"->"` (if the path isn't empty) and the node's value.
3. If the node is a leaf, add the path to the answer and return.
4. Otherwise recurse into the left and right children with the extended path (strings are immutable, so no undo step is needed).

## Code Implementation
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def binaryTreePaths(self, root: Optional[TreeNode]) -> list[str]:
        ans = []

        def dfs(node: Optional[TreeNode], path: str) -> None:
            if not node:
                return
            path = f"{path}->{node.val}" if path else str(node.val)
            if not node.left and not node.right:
                ans.append(path)
                return
            dfs(node.left, path)
            dfs(node.right, path)

        dfs(root, "")
        return ans
```

## Time Complexity Analysis
> Time complexity  : O(n * h) — the path string (length O(h)) is copied at every node, where h is the tree height
>
> Space complexity : O(n * h) — the output paths plus the path copies on the recursion stack

## Related Problems
- [112. Path Sum](https://leetcode.com/problems/path-sum) — 🟢 Easy · root-to-leaf DFS carrying state
- [113. Path Sum II](https://leetcode.com/problems/path-sum-ii) — 🟡 Medium · collect every root-to-leaf path matching a condition
- [144. Binary Tree Preorder Traversal](./144_binary_tree_preorder_traversal.md) — 🟢 Easy · the path is built in preorder
