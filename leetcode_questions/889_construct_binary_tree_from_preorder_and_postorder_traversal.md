# 889. Construct Binary Tree from Preorder and Postorder Traversal

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/)

## Question Description
Given two integer arrays, preorder and postorder where preorder is the preorder traversal of a binary tree of distinct values and postorder is the postorder traversal of the same tree, reconstruct and return the binary tree.

If there exist multiple answers, you can return any of them.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/07/24/lc-prepost.jpg" width="300" />
>
> Input: preorder = [1,2,4,5,3,6,7], postorder = [4,5,2,6,7,3,1]
>
> Output: [1,2,3,4,5,6,7]

Example 2:
>
> Input: preorder = [1], postorder = [1]
>
> Output: [1]

Constraints:
- 1 <= preorder.length <= 30
- 1 <= preorder[i] <= preorder.length
- All the values of preorder are unique.
- postorder.length == preorder.length
- 1 <= postorder[i] <= postorder.length
- All the values of postorder are unique.
- It is guaranteed that preorder and postorder are the preorder traversal and postorder traversal of the same binary tree.

## Tags
- tree

## Approach
**Key idea:** `preorder[0]` is the root and `preorder[1]` is the root of the left subtree. In postorder, that left root is the last node of the left subtree, so its position tells you how big the left subtree is.

1. Map each value to its index in `postorder` for O(1) lookups.
2. Recursively build from a preorder range `[pre_l, pre_r]` and the matching postorder start `post_l`.
3. The first preorder value is the root; if the range has one node, return it as a leaf.
4. Find `preorder[pre_l + 1]` in postorder: `left_size = index - post_l + 1`.
5. Build the left subtree from the next `left_size` preorder values and the right subtree from the rest.

## Code Implementation
```python
from typing import Optional

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def constructFromPrePost(self, preorder: list[int], postorder: list[int]) -> Optional[TreeNode]:
        post_idx = {v: i for i, v in enumerate(postorder)}

        def build(pre_l: int, pre_r: int, post_l: int) -> Optional[TreeNode]:
            if pre_l > pre_r:
                return None
            root = TreeNode(preorder[pre_l])
            if pre_l == pre_r:
                return root
            # The left child's root is the last node of the left subtree in postorder
            left_size = post_idx[preorder[pre_l + 1]] - post_l + 1
            root.left = build(pre_l + 1, pre_l + left_size, post_l)
            root.right = build(pre_l + left_size + 1, pre_r, post_l + left_size)
            return root

        return build(0, len(preorder) - 1, 0)
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node is created once, with O(1) index lookups
>
> Space complexity : O(n) — the index map, plus O(h) recursion stack

## Related Problems
- [105. Construct Binary Tree from Preorder and Inorder Traversal](./105_construct_binary_tree_from_preorder_and_inorder_traversal.md) — 🟡 Medium · same divide-by-subtree-size idea with inorder
- [106. Construct Binary Tree from Inorder and Postorder Traversal](./106_construct_binary_tree_from_inorder_and_postorder_traversal.md) — 🟡 Medium · same technique, different traversal pair
- [1008. Construct Binary Search Tree from Preorder Traversal](./1008_construct_binary_search_tree_from_preorder_traversal.md) — 🟡 Medium · rebuild a tree from one traversal using BST order
