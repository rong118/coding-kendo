# 106. Construct Binary Tree from Inorder and Postorder Traversal

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

## Question Description
Given two integer arrays inorder and postorder where inorder is the inorder traversal of a binary tree and postorder is the postorder traversal of the same tree, construct and return the binary tree.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/02/19/tree.jpg" width="300" />
>
> Input: inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]
> 
> Output: [3,9,20,null,null,15,7]

Example 2:
> Input: inorder = [-1], postorder = [-1]
>
> Output: [-1]


Constraints:
- 1 <= inorder.length <= 3000
- postorder.length == inorder.length
- -3000 <= inorder[i], postorder[i] <= 3000
- inorder and postorder consist of unique values.
- Each value of postorder also appears in inorder.
- inorder is guaranteed to be the inorder traversal of the tree.
- postorder is guaranteed to be the postorder traversal of the tree.

## Tags
- tree

## Approach
**Key idea:** The last element of postorder is the root; its position in inorder splits the remaining values into the left and right subtrees.

1. Build a hash map from value to its index in `inorder` for O(1) lookups.
2. Keep a pointer at the end of `postorder`; each recursive call consumes the value it points to as the subtree root.
3. Find the root's inorder index `mid`; values in `[start, mid - 1]` form the left subtree and `[mid + 1, end]` form the right.
4. Build the **right** subtree first, because reading postorder backwards yields root, right, then left.
5. Return `None` when `start > end`.

## Code Implementation
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, inorder: list[int], postorder: list[int]) -> Optional[TreeNode]:
        index = {v: i for i, v in enumerate(inorder)}
        post_idx = len(postorder) - 1

        def helper(start: int, end: int) -> Optional[TreeNode]:
            nonlocal post_idx
            if start > end:
                return None
            val = postorder[post_idx]
            post_idx -= 1
            root = TreeNode(val)
            mid = index[val]
            root.right = helper(mid + 1, end)
            root.left = helper(start, mid - 1)
            return root

        return helper(0, len(inorder) - 1)
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node is created once with an O(1) index lookup
>
> Space complexity : O(n) — hash map plus recursion stack

## Related Problems
- [105. Construct Binary Tree from Preorder and Inorder Traversal](./105_construct_binary_tree_from_preorder_and_inorder_traversal.md) — 🟡 Medium · mirror problem reading preorder forwards
- [889. Construct Binary Tree from Preorder and Postorder Traversal](./889_construct_binary_tree_from_preorder_and_postorder_traversal.md) — 🟡 Medium · rebuild from a different traversal pair
- [1008. Construct Binary Search Tree from Preorder Traversal](./1008_construct_binary_search_tree_from_preorder_traversal.md) — 🟡 Medium · rebuild a tree from one traversal using BST bounds
