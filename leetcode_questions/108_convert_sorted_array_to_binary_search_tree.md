# 108. Convert Sorted Array to Binary Search Tree

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)

## Question Description
Given an integer array nums where the elements are sorted in ascending order, convert it to a height-balanced binary search tree.

A height-balanced binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

<br/>

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/02/18/btree1.jpg" width="400" />
>
> Input: nums = [-10,-3,0,5,9]
>
> Output: [0,-3,9,-10,null,5]
>
> Explanation: [0,-10,5,null,-3,null,9] is also accepted:

Example 2:
> <img src="https://assets.leetcode.com/uploads/2021/02/18/btree.jpg" width="400" />
>
> Input: nums = [1,3]
>
> Output: [3,1]
>
> Explanation: [1,3] and [3,1] are both a height-balanced BSTs.

Constraints:
- 1 <= nums.length <= 10<sup>4</sup> 
- -10<sup>4</sup>  <= nums[i] <= 10<sup>4</sup> 
- nums is sorted in a strictly increasing order.

## Tags
- tree

## Approach
**Key idea:** The middle element of a sorted range splits it into two halves of (almost) equal size, so making it the root and recursing on each half yields a height-balanced BST.

1. Recurse on an index range `[lo, hi]`, starting with the whole array.
2. If `lo > hi`, the range is empty — return `None`.
3. Make `nums[mid]` the root, where `mid = (lo + hi) // 2`.
4. Build the left subtree from `[lo, mid - 1]` and the right subtree from `[mid + 1, hi]`.

## Code Implementation
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sortedArrayToBST(self, nums: list[int]) -> Optional[TreeNode]:
        def build(lo: int, hi: int) -> Optional[TreeNode]:
            if lo > hi:
                return None
            mid = (lo + hi) // 2
            root = TreeNode(nums[mid])
            root.left = build(lo, mid - 1)
            root.right = build(mid + 1, hi)
            return root

        return build(0, len(nums) - 1)
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(log n) — recursion depth of a balanced tree (O(n) including the output tree)

## Related Problems
- [1382. Balance a Binary Search Tree](./1382_balance_a_binary_search_tree.md) — 🟡 Medium · inorder to a sorted array, then the same middle-root build
- [1008. Construct Binary Search Tree from Preorder Traversal](./1008_construct_binary_search_tree_from_preorder_traversal.md) — 🟡 Medium · building a BST from a traversal
- [109. Convert Sorted List to Binary Search Tree](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree) — 🟡 Medium · same idea on a linked list
- [96. Unique Binary Search Trees](./96_unique_binary_search_trees.md) — 🟡 Medium · choosing a root splits values into left/right subtrees
