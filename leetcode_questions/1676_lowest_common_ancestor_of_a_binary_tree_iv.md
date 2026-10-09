# 1676 Lowest Common Ancestor of a Binary Tree IV

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-iv/)

## Question Description
Given the root of a binary tree and an array of TreeNode objects nodes, return the lowest common ancestor (LCA) of all the nodes in nodes. All the nodes will exist in the tree, and all values of the tree's nodes are unique.

Extending the definition of LCA on Wikipedia: "The lowest common ancestor of n nodes p1, p2, ..., pn in a binary tree T is the lowest node that has every pias a descendant (where we allow a node to be a descendant of itself) for every valid i". A descendant of a node x is a node y that is on the path from node xto some leaf node.

Example 1:
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], nodes = [4,7]
>
> Output: 2
>
> Explanation: The lowest common ancestor of nodes 4 and 7 is node 2.

Example 2:
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], nodes = [1]
>
> Output: 1
>
> Explanation: The lowest common ancestor of a single node is the node itself.

Example 3:
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], nodes = [7,6,2,4]
>
> Output: 5
> Explanation: The lowest common ancestor of the nodes 7, 6, 2, and 4 is node 5.

Example 4:
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], nodes = [0,1,2,3,4,5,6,7,8]
> Output: 3
> Explanation: The lowest common ancestor of all the nodes is the root node.

Constraints:
- The number of nodes in the tree is in the range [1, 10<sup>4</sup>].
- -10<sup>4</sup> <= Node.val <= 10<sup>4</sup> 
- All Node.val are unique.
- All nodes[i] will exist in the tree.
- All nodes[i] are distinct.

## Tags
- tree

## Approach
**Key idea:** Generalize the classic two-node LCA: put all targets in a set; a subtree returns a target as soon as it hits one, and the first node that receives non-null results from both sides is the LCA.

1. Store all target nodes in a hash set for O(1) lookups.
2. DFS: if the node is null or is a target, return it (a target is an ancestor of every target below it).
3. Otherwise recurse into the left and right subtrees.
4. If both sides return a node, targets are split across this node, so it is the LCA; otherwise pass up whichever side is non-null.

## Code Implementation
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', nodes: 'list[TreeNode]') -> 'TreeNode':
        targets = set(nodes)

        def dfs(node: Optional[TreeNode]) -> Optional[TreeNode]:
            if not node or node in targets:
                return node
            l = dfs(node.left)
            r = dfs(node.right)
            if l and r:
                return node
            return l or r

        return dfs(root)
```

## Time Complexity Analysis
> Time complexity  : O(n + m) — each tree node is visited once, plus building the set of m target nodes
>
> Space complexity : O(h + m) — recursion depth h plus the target set

## Related Problems
- [236. Lowest Common Ancestor of a Binary Tree](./236_lowest_common_ancestor_of_a_binary_tree.md) — 🟡 Medium · the two-node version of the same DFS
- [1644. Lowest Common Ancestor of a Binary Tree II](./1644_lowest_common_ancestor_of_a_binary_tree_ii.md) — 🟡 Medium · targets may not exist in the tree
- [1650. Lowest Common Ancestor of a Binary Tree III](./1650_lowest_common_ancestor_of_a_binary_tree_iii.md) — 🟡 Medium · LCA using parent pointers
- [235. Lowest Common Ancestor of a Binary Search Tree](./235_lowest_common_ancestor_of_a_binary_search_tree.md) — 🟡 Medium · LCA using BST ordering
