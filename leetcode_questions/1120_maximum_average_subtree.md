# 1120. Maximum Average Subtree

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/maximum-average-subtree/)

## Question Description
Given the root of a binary tree, find the maximum average value of any subtree of that tree.

(A subtree of a tree is any node of that tree plus all its descendants. The average value of a tree is the sum of its values, divided by the number of nodes.) 

Example 1:
>
> Input: [5,6,1]
>
> Output: 6.00000
>
> Explanation: 
>
> For the node with value = 5 we have an average of (5 + 6 + 1) / 3 = 4.
>
> For the node with value = 6 we have an average of 6 / 1 = 6.
>
> For the node with value = 1 we have an average of 1 / 1 = 1.
>
> So the answer is 6 which is the maximum.

Note:
- The number of nodes in the tree is between 1 and 5000.
- Each node will have a value between 0 and 100000.
- Answers will be accepted as correct if they are within 10^-5 of the correct answer.

<br/>

## Tags
- tree

## Approach
**Key idea:** A subtree's average needs its sum and node count, and both are just the children's values plus the current node — so one post-order pass computes every subtree's average.

1. DFS returns `(sum, count)` for each subtree; an empty subtree is `(0, 0)`.
2. Combine the children: `sum = left_sum + right_sum + node.val`, `count = left_count + right_count + 1`.
3. Update the best answer with `sum / count`.
4. Return `(sum, count)` to the parent.

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
    def maximumAverageSubtree(self, root: Optional[TreeNode]) -> float:
        best = 0.0

        def dfs(node: Optional[TreeNode]) -> tuple[int, int]:
            """Return (sum, count) of the subtree rooted at node."""
            nonlocal best
            if not node:
                return 0, 0
            ls, lc = dfs(node.left)
            rs, rc = dfs(node.right)
            total, count = ls + rs + node.val, lc + rc + 1
            best = max(best, total / count)
            return total, count

        dfs(root)
        return best
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(h) — recursion stack, h = tree height

## Related Problems
- [124. Binary Tree Maximum Path Sum](./124_binary_tree_maximum_path_sum.md) — 🔴 Hard · post-order DFS with a global best
- [1448. Count Good Nodes in Binary Tree](./1448_count_good_nodes_in_binary_tree.md) — 🟡 Medium · per-node check during DFS
- [2265. Count Nodes Equal to Average of Subtree](https://leetcode.com/problems/count-nodes-equal-to-average-of-subtree) — 🟡 Medium · same (sum, count) post-order DFS
