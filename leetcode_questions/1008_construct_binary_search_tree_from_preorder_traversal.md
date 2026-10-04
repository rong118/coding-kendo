# 1008. Construct Binary Search Tree from Preorder Traversal

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/)

## Question Description
Given an array of integers preorder, which represents the preorder traversal of a BST (i.e., binary search tree), construct the tree and return its root.

It is guaranteed that there is always possible to find a binary search tree with the given requirements for the given test cases.

A binary search tree is a binary tree where for every node, any descendant of Node.left has a value strictly less than Node.val, and any descendant of Node.right has a value strictly greater than Node.val.

A preorder traversal of a binary tree displays the value of the node first, then traverses Node.left, then traverses Node.right.

Example 1:
>
> <img src="https://assets.leetcode.com/uploads/2019/03/06/1266.png" width="400" />
>
> Input: preorder = [8,5,1,7,10,12]
>
> Output: [8,5,10,1,7,null,12]

Example 2:
>
> Input: preorder = [1,3]
>
> Output: [1,null,3]

Constraints:
- 1 <= preorder.length <= 100
- 1 <= preorder[i] <= 1000
- All the values of preorder are unique.

## Tags
- tree

## Approach
**Key idea:** In preorder the first value is the root, and the values that belong to each subtree are exactly those that fit the bounds set by the BST property — so one left-to-right pass with bounds rebuilds the tree.

1. Keep a shared index into `preorder`, starting at 0.
2. `build(lower, upper)`: if the index is past the end or the next value is outside `(lower, upper)`, return `None`.
3. Otherwise create a node from that value and advance the index.
4. Build its left subtree with bounds `(lower, val)` and its right subtree with `(val, upper)`.
5. Call `build(-inf, +inf)` for the root.

## Code Implementation
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def bstFromPreorder(self, preorder: list[int]) -> Optional[TreeNode]:
        idx = 0

        def build(lower: float, upper: float) -> Optional[TreeNode]:
            nonlocal idx
            if idx == len(preorder) or not (lower < preorder[idx] < upper):
                return None
            val = preorder[idx]
            idx += 1
            node = TreeNode(val)
            node.left = build(lower, val)
            node.right = build(val, upper)
            return node

        return build(float('-inf'), float('inf'))
```

## Time Complexity Analysis
> Time complexity  : O(n) — each value is consumed once
>
> Space complexity : O(n) — the output tree; recursion uses O(h)

## Related Problems
- [449. Serialize and Deserialize BST](./449_serialize_and_deserialize_BST.md) — 🟡 Medium · same bounded preorder rebuild
- [105. Construct Binary Tree from Preorder and Inorder Traversal](./105_construct_binary_tree_from_preorder_and_inorder_traversal.md) — 🟡 Medium · rebuild a general tree from traversals
- [889. Construct Binary Tree from Preorder and Postorder Traversal](./889_construct_binary_tree_from_preorder_and_postorder_traversal.md) — 🟡 Medium · rebuild from traversals
- [108. Convert Sorted Array to Binary Search Tree](./108_convert_sorted_array_to_binary_search_tree.md) — 🟢 Easy · build a BST from a sorted sequence
