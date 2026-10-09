# 94. Binary Tree Inorder Traversal

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/binary-tree-inorder-traversal/)

## Question Description
Given the root of a binary tree, return the inorder traversal of its nodes' values.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg" width="400" />
> 
> Input: root = [1,null,2,3]
> 
> Output: [1,3,2]

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
> Output: [2,1]

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
**Key idea:** Inorder means left subtree, then the node, then the right subtree; this can be done with recursion or by simulating the call stack with an explicit stack.

1. **Recursive:** visit `left`, append `node.val`, visit `right`; stop at `None`.
2. **Iterative:** starting from `root`, push nodes while walking left until reaching `None`.
3. Pop the top node — it is the next in inorder — and append its value.
4. Move to that node's right child and repeat until both the current node and the stack are empty.

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
    def inorderTraversal(self, root: Optional[TreeNode]) -> list[int]:
        res = []

        def helper(node: Optional[TreeNode]) -> None:
            if not node:
                return
            helper(node.left)
            res.append(node.val)
            helper(node.right)

        helper(root)
        return res
```

### Approach 2: Iterative (Stack)
```python
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> list[int]:
        res = []
        stack = []
        while root or stack:
            while root:
                stack.append(root)
                root = root.left
            root = stack.pop()
            res.append(root.val)
            root = root.right
        return res
```

## Time Complexity Analysis
> Time complexity  : O(n) — every node is visited once
>
> Space complexity : O(h) — recursion / explicit stack, where h is the tree height (O(n) worst case)

## Related Problems
- [144. Binary Tree Preorder Traversal](./144_binary_tree_preorder_traversal.md) — 🟢 Easy · same DFS, different visit order
- [145. Binary Tree Postorder Traversal](./145_binary_tree_postorder_traversal.md) — 🟢 Easy · same DFS, different visit order
- [173. Binary Search Tree Iterator](./173_binary_search_tree_iterator.md) — 🟡 Medium · the iterative stack traversal, made lazy
- [98. Validate Binary Search Tree](./98_validate_binary_search_tree.md) — 🟡 Medium · inorder of a BST is sorted
