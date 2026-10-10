# 145. Binary Tree Postorder Traversal

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/binary-tree-postorder-traversal/)

## Question Description
Given the root of a binary tree, return the postorder traversal of its nodes' values.

Example 1:
Input: root = [1,null,2,3]
Output: [3,2,1]

Example 2:
Input: root = []
Output: []

Example 3:
Input: root = [1]
Output: [1]

Example 4:
Input: root = [1,2]
Output: [2,1]

Example 5:
Input: root = [1,null,2]
Output: [2,1]



Example
> example's description

Constraints:
- The number of the nodes in the tree is in the range [0, 100].
- -100 <= Node.val <= 100

## Tags

## Approach
**Key idea:** Postorder is left → right → root. Recursion follows that directly; iteratively, a root → right → left preorder is exactly postorder reversed.

1. Recursive: visit the left subtree, then the right subtree, then append the node's value.
2. Iterative: push the root on a stack.
3. Pop a node, append its value, then push its left child and then its right child (so the right is processed first).
4. When the stack is empty, reverse the collected values to get postorder.

## Code Implementation
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    # Recursive
    def postorderTraversal(self, root: Optional[TreeNode]) -> list[int]:
        res = []

        def dfs(node: Optional[TreeNode]) -> None:
            if not node:
                return
            dfs(node.left)
            dfs(node.right)
            res.append(node.val)

        dfs(root)
        return res

    # Iterative — root/right/left order, then reverse
    def postorderTraversalIterative(self, root: Optional[TreeNode]) -> list[int]:
        if not root:
            return []
        res = []
        stack = [root]
        while stack:
            node = stack.pop()
            res.append(node.val)
            if node.left:
                stack.append(node.left)
            if node.right:
                stack.append(node.right)
        return res[::-1]
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node is visited once
>
> Space complexity : O(h) recursive (call stack, h = tree height); O(n) iterative (explicit stack)

## Related Problems
- [94. Binary Tree Inorder Traversal](./94_binary_tree_inorder_traversal.md) — 🟢 Easy · sibling DFS traversal order
- [144. Binary Tree Preorder Traversal](./144_binary_tree_preorder_traversal.md) — 🟢 Easy · iterative postorder is reversed modified preorder
- [102. Binary Tree Level Order Traversal](./102_binary_tree_level_order_traversal.md) — 🟡 Medium · BFS counterpart of the DFS traversals
