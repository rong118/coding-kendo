# 1382. Balance a Binary Search Tree

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/balance-a-binary-search-tree/)

## Question Description
Given the root of a binary search tree, return a balanced binary search tree with the same node values. If there is more than one answer, return any of them.

A binary search tree is balanced if the depth of the two subtrees of every node never differs by more than 1

<br/>

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/08/10/balance1-tree.jpg" width="400" />
>
> Input: root = [1,null,2,null,3,null,4,null,null]
>
> Output: [2,1,3,null,null,null,4]
>
> Explanation: This is not the only correct answer, [3,1,4,null,2] is also correct.

Example 2:
> <img src="https://assets.leetcode.com/uploads/2021/08/10/balanced2-tree.jpg" width="400" />
>
> Input: root = [2,1,3]
>
> Output: [2,1,3]

Constraints:
- The number of nodes in the tree is in the range [1, 10<sup>4</sup>].
- 1 <= Node.val <= 10<sup>5</sup> 

## Tags
- tree

## Approach
**Key idea:** An in-order traversal gives the values in sorted order, and building a tree by always choosing the middle element as root splits the remaining values evenly, which guarantees balance.

1. Collect the values with an in-order traversal (sorted).
2. Recursively build on the range `[lo, hi]`: pick `mid = (lo + hi) // 2` as the root.
3. Build the left subtree from `[lo, mid - 1]` and the right from `[mid + 1, hi]`.
4. Return `None` for an empty range.

## Code Implementation
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

from typing import Optional


class Solution:
    def balanceBST(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        vals: list[int] = []

        def inorder(node: Optional[TreeNode]) -> None:
            if not node:
                return
            inorder(node.left)
            vals.append(node.val)
            inorder(node.right)

        def build(lo: int, hi: int) -> Optional[TreeNode]:
            if lo > hi:
                return None
            mid = (lo + hi) // 2
            return TreeNode(vals[mid], build(lo, mid - 1), build(mid + 1, hi))

        inorder(root)
        return build(0, len(vals) - 1)
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(n) — sorted value list and the new tree

## Related Problems
- [108. Convert Sorted Array to Binary Search Tree](./108_convert_sorted_array_to_binary_search_tree.md) — 🟢 Easy · the build-from-middle step on its own
- [94. Binary Tree Inorder Traversal](./94_binary_tree_inorder_traversal.md) — 🟢 Easy · the flatten-to-sorted step
- [110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree) — 🟢 Easy · check the balance property this produces
