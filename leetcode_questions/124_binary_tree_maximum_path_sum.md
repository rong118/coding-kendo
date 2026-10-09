# 124. Binary Tree Maximum Path Sum

**Difficulty:** 🔴 Hard

## Question link
(https://leetcode.com/problems/binary-tree-maximum-path-sum/)

## Question Description
A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence at most once. Note that the path does not need to pass through the root.

The path sum of a path is the sum of the node's values in the path.

Given the root of a binary tree, return the maximum path sum of any non-empty path.


Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/10/13/exx1.jpg" width="400" />
>
> Input: root = [1,2,3]
>
> Output: 6
>
> Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.

Example 2:
> <img src="https://assets.leetcode.com/uploads/2020/10/13/exx2.jpg" width="400" />
>
> Input: root = [-10,9,20,null,null,15,7]
>
> Output: 42
>
> Explanation: The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.

<br/>

Example
> example's description

Constraints:
- The number of nodes in the tree is in the range [1, 3 * 10<sup>4</sup>].
- -1000 <= Node.val <= 1000

## Tags
- tree
- dfs

## Approach
**Key idea:** Every path has a single highest node where it "bends"; at that node the path is `node.val + best left branch + best right branch`, while a parent can only extend one of those branches.

1. Post-order DFS returns the best downward path sum starting at each node.
2. Clamp each child's gain at 0 — a negative branch is better left out.
3. Update the global answer with `node.val + left + right` (the path that bends here).
4. Return `node.val + max(left, right)` to the parent.
5. Start the answer at negative infinity so all-negative trees return their largest node.

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
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        best = float("-inf")

        def gain(node: Optional[TreeNode]) -> int:
            """Best sum of a downward path starting at node."""
            nonlocal best
            if not node:
                return 0
            left = max(0, gain(node.left))    # drop negative branches
            right = max(0, gain(node.right))
            best = max(best, node.val + left + right)  # path bending at node
            return node.val + max(left, right)          # extend only one side upward

        gain(root)
        return best
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(h) — recursion stack, h = tree height

## Related Problems
- [549. Binary Tree Longest Consecutive Sequence II](./549_binary_tree_longest_consecutive_sequence_ii.md) — 🟡 Medium · combine left and right downward results at each node
- [543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree) — 🟢 Easy · same bend-at-a-node pattern, counting edges
- [687. Longest Univalue Path](https://leetcode.com/problems/longest-univalue-path) — 🟡 Medium · same pattern with an equal-value constraint
