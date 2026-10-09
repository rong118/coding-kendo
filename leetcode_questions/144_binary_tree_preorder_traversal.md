# 144. Binary Tree Preorder Traversal

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/binary-tree-preorder-traversal/)

## Question Description
Given the root of a binary tree, return the preorder traversal of its nodes' values.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg" width="400" /> 
> Input: root = [1,null,2,3]
>
> Output: [1,2,3]

Example 2:
> Input: root = []
>
> Output: []

Example 3:
> Input: root = [1]
>
> Output: [1]

Example 4:
> Input: root = [1,2]
>
> Output: [1,2]

Example 5:
> Input: root = [1,null,2]
>
> Output: [1,2]

Constraints:
- The number of nodes in the tree is in the range [0, 100].
- -100 <= Node.val <= 100

## Tags
- tree

## Approach
**Key idea:** Preorder visits root, then left, then right. Recursion expresses this directly; iteratively, a stack works if you push the right child before the left so the left subtree is popped (visited) first.

1. If the tree is empty, return an empty list.
2. Recursive: record the node's value, then recurse into the left subtree, then the right subtree.
3. Iterative: push the root onto a stack, then repeatedly pop a node and record its value.
4. After popping, push its right child and then its left child (if present), so the left one comes off the stack next.

## Code Implementation
### Approach 1: Recursive
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> list[int]:
        res = []

        def dfs(node: Optional[TreeNode]) -> None:
            if not node:
                return
            res.append(node.val)
            dfs(node.left)
            dfs(node.right)

        dfs(root)
        return res
```

### Approach 2: Iterative with a Stack
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def preorderTraversal(self, root: Optional[TreeNode]) -> list[int]:
        if not root:
            return []
        res, stack = [], [root]
        while stack:
            node = stack.pop()
            res.append(node.val)
            # push right first so the left subtree is processed first
            if node.right:
                stack.append(node.right)
            if node.left:
                stack.append(node.left)
        return res
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(h) — recursion depth / stack size, where h is the tree height (O(n) worst case)

## Related Problems
- [94. Binary Tree Inorder Traversal](./94_binary_tree_inorder_traversal.md) — 🟢 Easy · same traversal family, recursive and stack-based
- [145. Binary Tree Postorder Traversal](./145_binary_tree_postorder_traversal.md) — 🟢 Easy · same traversal family, recursive and stack-based
- [102. Binary Tree Level Order Traversal](./102_binary_tree_level_order_traversal.md) — 🟡 Medium · BFS counterpart using a queue
