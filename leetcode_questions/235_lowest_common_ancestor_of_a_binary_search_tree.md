# 235. Lowest Common Ancestor of a Binary Search Tree

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

## Question Description
Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

Example 1:
> <img src="https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png" width="400" />
>
> Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
>
> Output: 6
>
> Explanation: The LCA of nodes 2 and 8 is 6.

Example 2:
> Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
>
> Output: 2
>
> Explanation: The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.

Example 3:
> Input: root = [2,1], p = 2, q = 1
>
> Output: 2

<br/>

Constraints:
- The number of nodes in the tree is in the range [2, 10<sup>5</sup>].
- -109 <= Node.val <= 109
- All Node.val are unique.
- p != q
- p and q will exist in the BST.

## Tags
- tree
- bst

## Approach
**Key idea:** In a BST, if `p` and `q` are both smaller than the current node the LCA is in the left subtree, and if both are larger it is in the right subtree; otherwise the current node is where they split, so it is the LCA.

1. Start at the root.
2. If both `p.val` and `q.val` are less than `root.val`, recurse into the left subtree.
3. If both are greater than `root.val`, recurse into the right subtree.
4. Otherwise `p` and `q` are on different sides (or one of them is `root`), so return `root`.

## Code Implementation
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if not root:
            return None
        if p.val < root.val and q.val < root.val:
            return self.lowestCommonAncestor(root.left, p, q)
        if p.val > root.val and q.val > root.val:
            return self.lowestCommonAncestor(root.right, p, q)
        return root
```

## Time Complexity Analysis
> Time complexity  : O(h) — one root-to-node path; O(log n) for a balanced BST, O(n) in the worst case
>
> Space complexity : O(h) — recursion stack

## Related Problems
- [236. Lowest Common Ancestor of a Binary Tree](./236_lowest_common_ancestor_of_a_binary_tree.md) — 🟡 Medium · same question without BST ordering
- [1650. Lowest Common Ancestor of a Binary Tree III](./1650_lowest_common_ancestor_of_a_binary_tree_iii.md) — 🟡 Medium · LCA using parent pointers
- [270. Closest Binary Search Tree Value](./270_closest_binary_search_tree_value.md) — 🟢 Easy · walks one BST path guided by value comparisons
