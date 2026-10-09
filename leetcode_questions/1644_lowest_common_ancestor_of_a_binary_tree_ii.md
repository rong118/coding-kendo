# 1644. Lowest Common Ancestor of a Binary Tree II

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-ii/)

## Question Description
Given the root of a binary tree, return the lowest common ancestor (LCA) of two given nodes, p and q. If either node p or q does not exist in the tree, return null. All values of the nodes in the tree are unique.
According to the definition of LCA on Wikipedia: "The lowest common ancestor of two nodes p and q in a binary tree T is the lowest node that has both p and q as descendants (where we allow a node to be a descendant of itself)". A descendant of a node x is a node y that is on the path from node x to some leaf node.

Example 1:
>
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
>
> Output: 3
>
> Explanation: The LCA of nodes 5 and 1 is 3.

Example 2:
>
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
>
> Output: 5
>
> Explanation: The LCA of nodes 5 and 4 is 5. A node can be a descendant of itself according to the definition of LCA.

Example 3:
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 10
>
> Output: null
>
> Explanation: Node 10 does not exist in the tree, so return null.

Constraints:
- The number of nodes in the tree is in the range [1, 10<sup>4</sup>].
- -10<sup>9</sup> <= Node.val <= 10<sup>9</sup> 
- All Node.val are unique.
- p != q

Follow up: Can you find the LCA traversing the tree, without checking nodes existence?

<br/>

## Tags
- tree
- bst

## Approach
**Key idea:** The classic LCA recursion assumes both nodes exist, so first verify that `p` and `q` are both in the tree, then run the standard LCA search.

1. DFS to check that `p` exists in the tree; do the same for `q`. If either is missing, return `None`.
2. Run the standard LCA: if the current node is `None`, `p`, or `q`, return it.
3. Recurse into the left and right subtrees.
4. If both sides return a node, the current node is the LCA; otherwise pass up whichever side is non-null.

## Code Implementation
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
class Solution:
    def lowestCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) -> Optional[TreeNode]:
        def exists(node: Optional[TreeNode], target: TreeNode) -> bool:
            if not node:
                return False
            if node is target:
                return True
            return exists(node.left, target) or exists(node.right, target)

        def lca(node: Optional[TreeNode]) -> Optional[TreeNode]:
            if not node or node is p or node is q:
                return node
            left = lca(node.left)
            right = lca(node.right)
            if left and right:
                return node
            return left or right

        if exists(root, p) and exists(root, q):
            return lca(root)
        return None
```

## Time Complexity Analysis
> Time complexity  : O(n) — at most three full traversals
>
> Space complexity : O(h) — recursion depth, where h is the tree height (O(n) worst case)

## Related Problems
- [236. Lowest Common Ancestor of a Binary Tree](./236_lowest_common_ancestor_of_a_binary_tree.md) — 🟡 Medium · the base LCA where both nodes exist
- [1650. Lowest Common Ancestor of a Binary Tree III](./1650_lowest_common_ancestor_of_a_binary_tree_iii.md) — 🟡 Medium · LCA using parent pointers
- [1676. Lowest Common Ancestor of a Binary Tree IV](./1676_lowest_common_ancestor_of_a_binary_tree_iv.md) — 🟡 Medium · LCA of many nodes
- [235. Lowest Common Ancestor of a Binary Search Tree](./235_lowest_common_ancestor_of_a_binary_search_tree.md) — 🟡 Medium · LCA using BST ordering
