# 98. Validate Binary Search Tree

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/validate-binary-search-tree/)

## Question Description
Given the root of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:
- The left subtree of a node contains only nodes with keys less than the node's key.
- The right subtree of a node contains only nodes with keys greater than the node's key.
- Both the left and right subtrees must also be binary search trees.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg" width="400" />
>
> Input: root = [2,1,3]
>
> Output: true

Example 2:
> <img src="https://assets.leetcode.com/uploads/2020/12/01/tree2.jpg" width="400" />
> 
> Input: root = [5,1,4,null,null,3,6]
>
> Output: false
>
> Explanation: The root node's value is 5 but its right child's value is 4.

Constraints:
- The number of nodes in the tree is in the range [1, 10<sup>4</sup>].
- -2<sup>31</sup> <= Node.val <= 2<sup>31</sup> - 1

## Tags
- tree
- bst

## Approach
**Key idea:** Every node must lie strictly inside an open interval set by its ancestors; equivalently, an in-order traversal of a valid BST is strictly increasing.

1. Recursive: start with the bounds `(-inf, +inf)` at the root.
2. If a node's value is not strictly between its bounds, the tree is invalid.
3. Recurse left with the upper bound tightened to the node's value, and right with the lower bound raised to it.
4. Iterative: do an in-order traversal with an explicit stack, remembering the previously visited value.
5. If any value is `<=` the previous one, return `False`; otherwise the tree is valid.

## Code Implementation
### Approach 1: Recursive bounds
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        def valid(node: Optional[TreeNode], low: float, high: float) -> bool:
            if not node:
                return True
            if not (low < node.val < high):
                return False
            return valid(node.left, low, node.val) and valid(node.right, node.val, high)

        return valid(root, float('-inf'), float('inf'))
```

### Approach 2: Iterative in-order
```python
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        stack = []
        prev = None
        node = root
        while node or stack:
            while node:
                stack.append(node)
                node = node.left
            node = stack.pop()
            if prev is not None and node.val <= prev:
                return False
            prev = node.val
            node = node.right
        return True
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node is visited once
>
> Space complexity : O(h) — recursion / explicit stack, where h is the tree height (O(n) worst case)

## Related Problems
- [94. Binary Tree Inorder Traversal](./94_binary_tree_inorder_traversal.md) — 🟢 Easy · in-order traversal of a BST is sorted
- [99. Recover Binary Search Tree](./99_recover_binary_search_tree.md) — 🟡 Medium · find in-order violations in a BST
- [173. Binary Search Tree Iterator](./173_binary_search_tree_iterator.md) — 🟡 Medium · iterative in-order with a stack
