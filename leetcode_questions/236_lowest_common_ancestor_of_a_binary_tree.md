# 236. Lowest Common Ancestor of a Binary Tree

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

## Question Description

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”


<img src="https://assets.leetcode.com/uploads/2018/12/14/binarytree.png" width="400" />

<br/>

Example 1:
> <img src="https://assets.leetcode.com/uploads/2018/12/14/binarytree.png" width="400" />
>
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
> Output: 3
> Explanation: The LCA of nodes 5 and 1 is 3.

Example 2:
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
>
> Output: 5
>
> Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.

Example 3:
> Input: root = [1,2], p = 1, q = 2
>
> Output: 1

Constraints:
- The number of nodes in the tree is in the range [2, 10<sup>5</sup>].
- -10<sup>9</sup> <= Node.val <= 10<sup>9</sup> 
- All Node.val are unique.
- p != q
- p and q will exist in the tree.

## Tags
- tree
- bst

## Approach
**Key idea:** A node is the LCA when `p` and `q` are found in different subtrees under it, or when it is one of them and the other is below it. Recursion can report upward where each target was found.

1. **Recursive:** if `root` is `None`, `p`, or `q`, return `root`.
2. Search the left and right subtrees.
3. If both sides return a node, `p` and `q` are split across `root`, so `root` is the LCA.
4. Otherwise return whichever side is non-empty; it holds the LCA (or the only target found so far).
5. **Parent map:** record each node's parent with a DFS, collect all ancestors of `p` in a set, then walk up from `q` until reaching one of them.

## Code Implementation
### Approach 1: Recursive (divide and conquer)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if root is None or root is p or root is q:
            return root
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        if left and right:
            return root
        return left or right
```

### Approach 2: Parent map

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        parent = {root: None}
        stack = [root]
        while stack:
            node = stack.pop()
            for child in (node.left, node.right):
                if child:
                    parent[child] = node
                    stack.append(child)

        ancestors = set()
        while p:
            ancestors.add(p)
            p = parent[p]
        while q not in ancestors:
            q = parent[q]
        return q
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node is visited once
>
> Space complexity : O(n) — recursion stack O(h), parent map O(n)

## Related Problems
- [235. Lowest Common Ancestor of a Binary Search Tree](./235_lowest_common_ancestor_of_a_binary_search_tree.md) — 🟡 Medium · BST ordering finds the split point directly
- [1644. Lowest Common Ancestor of a Binary Tree II](./1644_lowest_common_ancestor_of_a_binary_tree_ii.md) — 🟡 Medium · p or q may not exist
- [1650. Lowest Common Ancestor of a Binary Tree III](./1650_lowest_common_ancestor_of_a_binary_tree_iii.md) — 🟡 Medium · nodes have parent pointers
- [1676. Lowest Common Ancestor of a Binary Tree IV](./1676_lowest_common_ancestor_of_a_binary_tree_iv.md) — 🟡 Medium · LCA of many nodes
