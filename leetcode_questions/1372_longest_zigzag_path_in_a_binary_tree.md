# 1372. Longest ZigZag Path in a Binary Tree

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/longest-zigzag-path-in-a-binary-tree/)

## Question Description
You are given the root of a binary tree.

A ZigZag path for a binary tree is defined as follow:

- Choose any node in the binary tree and a direction (right or left).
- If the current direction is right, move to the right child of the current node; otherwise, move to the left child.
- Change the direction from right to left or from left to right.
- Repeat the second and third steps until you can't move in the tree.

Zigzag length is defined as the number of nodes visited - 1. (A single node has a length of 0).

Return the longest ZigZag path contained in that tree.

<br/>

Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/01/22/sample_1_1702.png" width="200" />
>
> Input: root = [1,null,1,1,1,null,null,1,1,null,1,null,null,null,1,null,1]
>
> Output: 3
>
> Explanation: Longest ZigZag path in blue nodes (right -> left -> right).

Example 2:
> <img src="https://assets.leetcode.com/uploads/2020/01/22/sample_2_1702.png" width="200" />
>
> Input: root = [1,1,1,null,1,null,null,1,1,null,1]
>
> Output: 4
>
> Explanation: Longest ZigZag path in blue nodes (left -> right -> left -> right).

Constraints:
- The number of nodes in the tree is in the range [1, 5 * 10<sup>4</sup>].
- 1 <= Node.val <= 100

## Tags
- tree
- dfs

## Approach
**Key idea:** For each node, the longest zigzag that starts by going left is 1 + the longest zigzag from its left child that continues by going right (and symmetrically for right), so one post-order DFS computes both directions for every node.

1. Let `dfs(node, is_left)` return the number of nodes on the zigzag path starting at `node`, given that `node` was entered by a left move (`is_left`) or a right move.
2. For a null node return `0`.
3. Compute `left = dfs(node.left, True)` and `right = dfs(node.right, False)`; these equal the edge counts of the zigzags from `node` going left and going right, so update the global answer with both.
4. Return `1 + right` if `node` was entered by a left move (the next move must be right), otherwise `1 + left`.
5. Run it from the root and return the best length found.

## Code Implementation
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def longestZigZag(self, root: Optional[TreeNode]) -> int:
        self.res = 0

        def dfs(node: Optional[TreeNode], is_left: bool) -> int:
            if not node:
                return 0
            left = dfs(node.left, True)     # zigzag from node going left
            right = dfs(node.right, False)  # zigzag from node going right
            self.res = max(self.res, left, right)
            return 1 + right if is_left else 1 + left

        dfs(root, True)
        return self.res
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(h) — recursion depth, where h is the tree height (O(n) worst case)

## Related Problems
- [124. Binary Tree Maximum Path Sum](./124_binary_tree_maximum_path_sum.md) — 🔴 Hard · post-order DFS returning a one-sided path while tracking a global best
- [549. Binary Tree Longest Consecutive Sequence II](./549_binary_tree_longest_consecutive_sequence_ii.md) — 🟡 Medium · per-node directional path lengths combined in one DFS
- [103. Binary Tree Zigzag Level Order Traversal](./103_binary_tree_zigzig_level_order_traversal.md) — 🟡 Medium · alternating direction in a tree
