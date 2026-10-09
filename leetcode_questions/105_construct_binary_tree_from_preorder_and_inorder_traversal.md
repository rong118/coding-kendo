# 105. Construct Binary Tree from Preorder and Inorder Traversal

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

## Question Description
Given two integer arrays preorder and inorder where preorder is the preorder traversal of a binary tree and inorder is the inorder traversal of the same tree, construct and return the binary tree.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/02/19/tree.jpg" width="300" />
>
> Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
>
> Output: [3,9,20,null,null,15,7]

Example 2:
> 
> Input: preorder = [-1], inorder = [-1]
>
> Output: [-1]

Constraints:
- 1 <= preorder.length <= 3000
- inorder.length == preorder.length
- -3000 <= preorder[i], inorder[i] <= 3000
- preorder and inorder consist of unique values.
- Each value of inorder also appears in preorder.
- preorder is guaranteed to be the preorder traversal of the tree.
- inorder is guaranteed to be the inorder traversal of the tree.

## Tags
- tree

## Approach
**Key idea:** The next value in preorder is always the root of the current subtree, and its position in inorder splits the remaining values into the left and right subtrees.

1. Build a hash map from value to index in `inorder` so each root can be found in O(1).
2. Keep a pointer `pre_idx` into `preorder`, starting at 0.
3. `helper(lo, hi)` builds the subtree for `inorder[lo..hi]`: return `None` if the range is empty.
4. Otherwise take `preorder[pre_idx]` as the root, advance the pointer, and find its inorder index `mid`.
5. Build the left subtree from `lo..mid-1` first (preorder visits left before right), then the right from `mid+1..hi`.

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
    def buildTree(self, preorder: list[int], inorder: list[int]) -> Optional[TreeNode]:
        index = {val: i for i, val in enumerate(inorder)}
        pre_idx = 0

        def helper(lo: int, hi: int) -> Optional[TreeNode]:
            nonlocal pre_idx
            if lo > hi:
                return None
            val = preorder[pre_idx]
            pre_idx += 1
            root = TreeNode(val)
            mid = index[val]
            root.left = helper(lo, mid - 1)
            root.right = helper(mid + 1, hi)
            return root

        return helper(0, len(inorder) - 1)
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node is created once with O(1) index lookup
>
> Space complexity : O(n) — hash map plus recursion stack

## Related Problems
- [106. Construct Binary Tree from Inorder and Postorder Traversal](./106_construct_binary_tree_from_inorder_and_postorder_traversal.md) — 🟡 Medium · same split, roots read from the end of postorder
- [889. Construct Binary Tree from Preorder and Postorder Traversal](./889_construct_binary_tree_from_preorder_and_postorder_traversal.md) — 🟡 Medium · rebuild a tree from two traversals
- [1008. Construct Binary Search Tree from Preorder Traversal](./1008_construct_binary_search_tree_from_preorder_traversal.md) — 🟡 Medium · preorder root consumption with value bounds
