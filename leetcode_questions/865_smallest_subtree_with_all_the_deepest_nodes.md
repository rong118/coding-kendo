# 865. Smallest Subtree with all the Deepest Nodes

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/smallest-subtree-with-all-the-deepest-nodes/)

## Question Description
Given the root of a binary tree, the depth of each node is the shortest distance to the root.

Return the smallest subtree such that it contains all the deepest nodes in the original tree.

A node is called the deepest if it has the largest depth possible among any node in the entire tree.

The subtree of a node is a tree consisting of that node, plus the set of all descendants of that node.

Example 1:
> <img src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/01/sketch1.png" width="400" />
>
> Input: root = [3,5,1,6,2,0,8,null,null,7,4]
>
> Output: [2,7,4]
>
> Explanation: We return the node with value 2, colored in yellow in the diagram.
>
> The nodes coloured in blue are the deepest nodes of the tree.
>
> Notice that nodes 5, 3 and 2 contain the deepest nodes in the tree but node 2 is the smallest subtree among them, so we return it.

Example 2:
>
>
> Input: root = [1]
>
> Output: [1]
>
> Explanation: The root is the deepest node in the tree.

Example 3:
> Input: root = [0,1,3,null,2]
>
> Output: [2]
>
> Explanation: The deepest node in the tree is 2, the valid subtrees are the subtrees of nodes 2, 1 and 0 but the subtree of node 2 is the smallest.
 

Constraints:
- The number of nodes in the tree will be in the range [1, 500].
- 0 <= Node.val <= 500
- The values of the nodes in the tree are unique.

<br/>

## Tags
- tree

## Approach
**Key idea:** If the left and right subtrees have equal height, the deepest nodes are split across both sides, so the current node is the answer; otherwise all deepest nodes are in the taller subtree, so recurse there.

1. Define `height(node)` = number of nodes on the longest path down (0 for `None`).
2. At the current node, compute the heights of its left and right subtrees.
3. If they are equal, return the current node.
4. Otherwise recurse into the taller side.

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
    def subtreeWithAllDeepest(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        def height(node: Optional[TreeNode]) -> int:
            if not node:
                return 0
            return 1 + max(height(node.left), height(node.right))

        node = root
        while node:
            lh, rh = height(node.left), height(node.right)
            if lh == rh:
                return node
            node = node.left if lh > rh else node.right
        return None
```

## Time Complexity Analysis
> Time complexity  : O(n · h) — each step down recomputes subtree heights; O(n log n) for a balanced tree, O(n²) worst case (skewed). A single post-order pass returning (depth, node) brings this to O(n), see [1123](./1123_lowest_common_ancestor_of_deepest_leaves.md).
>
> Space complexity : O(h) — recursion stack of the height computation

## Related Problems
- [1123. Lowest Common Ancestor of Deepest Leaves](./1123_lowest_common_ancestor_of_deepest_leaves.md) — 🟡 Medium · identical problem, includes the O(n) approach
- [236. Lowest Common Ancestor of a Binary Tree](./236_lowest_common_ancestor_of_a_binary_tree.md) — 🟡 Medium · classic LCA via post-order recursion
- [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree) — 🟢 Easy · the height helper used here
