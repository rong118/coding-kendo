# 270 Closest Binary Search Tree Value

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/closest-binary-search-tree-value/)

## Question Description
Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

Note:
Given target value is a floating point.
You are guaranteed to have only one unique value in the BST that is closest to the target.

Example:
>
> Input: root = [4,2,5,1,3], target = 3.714286
>
>    4
>   / \
>  2   5
> / \
>1   3
> Output: 4

## Tags
- tree
- bst

## Approach
**Key idea:** Like a BST search for `target`, the closest value must lie on the root-to-leaf search path, because each step discards a subtree whose values are all farther from `target` than the current node.

1. Start with `res = root.val`.
2. At each node, if it is at least as close to `target` as `res`, update `res`.
3. Go left if `target < node.val`, otherwise go right.
4. When the path ends (`None`), return `res`.

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
    def closestValue(self, root: Optional[TreeNode], target: float) -> int:
        res = root.val
        node = root
        while node:
            if abs(node.val - target) <= abs(res - target):
                res = node.val
            node = node.left if target < node.val else node.right
        return res
```

## Time Complexity Analysis
> Time complexity  : O(h) — one root-to-leaf path; O(log n) if balanced, O(n) worst case
>
> Space complexity : O(1)

## Related Problems
- [235. Lowest Common Ancestor of a Binary Search Tree](./235_lowest_common_ancestor_of_a_binary_search_tree.md) — 🟡 Medium · single-path walk guided by BST ordering
- [98. Validate Binary Search Tree](./98_validate_binary_search_tree.md) — 🟡 Medium · relies on the BST ordering property
- [272. Closest Binary Search Tree Value II](https://leetcode.com/problems/closest-binary-search-tree-value-ii) — 🔴 Hard · follow-up asking for the k closest values
- [700. Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree) — 🟢 Easy · the basic BST search this builds on
