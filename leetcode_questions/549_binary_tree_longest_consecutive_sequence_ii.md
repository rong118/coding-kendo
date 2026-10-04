# 549 Binary Tree Longest Consecutive Sequence II

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/binary-tree-longest-consecutive-sequence-ii/)

## Question Description
Given a binary tree, you need to find the length of Longest Consecutive Path in Binary Tree.

Especially, this path can be either increasing or decreasing. For example, [1,2,3,4] and [4,3,2,1] are both considered valid, but the path [1,2,4,3] is not valid. On the other hand, the path can be in the child-Parent-child order, where not necessarily be parent-child order.

Example 1:
>
> Input:
>
>        1
>       / \
>      2   3
>
> Output: 2
>
> Explanation: The longest consecutive path is [1, 2] or [2, 1].

Example 2:
> Input:
>
>        2
>       / \
>      1   3
>
> Output: 3
>
> Explanation: The longest consecutive path is [1, 2, 3] or [3, 2, 1].

<br/>

Note: All the values of tree nodes are in the range of [-1e7, 1e7].

## Tags
- tree
- dfs

## Approach
**Key idea:** Every consecutive path has a top node where it turns (child, parent, child). At that node the best path joins the longest increasing chain going down one side with the longest decreasing chain going down the other: `inc + dec - 1`.

1. Run a post-order DFS that returns `(inc, dec)` for each node: the longest increasing and decreasing downward paths that start at it.
2. Start both at 1 (the node itself).
3. For each child, if `child.val == node.val + 1` extend `inc` with the child's `inc`; if `child.val == node.val - 1` extend `dec` with the child's `dec`.
4. Update the answer with `inc + dec - 1` (the node is counted in both chains).
5. Return the best length after visiting every node.

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
    def longestConsecutive(self, root: Optional[TreeNode]) -> int:
        best = 0

        def dfs(node: Optional[TreeNode]) -> tuple[int, int]:
            # (inc, dec): longest increasing / decreasing downward path starting at node
            nonlocal best
            if not node:
                return 0, 0
            inc = dec = 1
            for child in (node.left, node.right):
                if not child:
                    continue
                c_inc, c_dec = dfs(child)
                if child.val == node.val + 1:
                    inc = max(inc, c_inc + 1)
                elif child.val == node.val - 1:
                    dec = max(dec, c_dec + 1)
            best = max(best, inc + dec - 1)
            return inc, dec

        dfs(root)
        return best
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node is visited once
>
> Space complexity : O(h) — recursion stack, where h is the tree height

## Related Problems
- [128. Longest Consecutive Sequence](./128_longest_consecutive_sequence.md) — 🟡 Medium · longest consecutive run in an unsorted array
- [298. Binary Tree Longest Consecutive Sequence](https://leetcode.com/problems/binary-tree-longest-consecutive-sequence) — 🟡 Medium · increasing parent-to-child paths only
- [124. Binary Tree Maximum Path Sum](./124_binary_tree_maximum_path_sum.md) — 🔴 Hard · same idea of joining two downward chains at a turning node
- [1372. Longest ZigZag Path in a Binary Tree](./1372_longest_zigzag_path_in_a_binary_tree.md) — 🟡 Medium · DFS returning per-direction path lengths
