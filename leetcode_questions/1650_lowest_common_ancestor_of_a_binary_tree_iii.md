# 1650 Lowest Common Ancestor of a Binary Tree III

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-iii/)

## Question Description
Given two nodes of a binary tree p and q, return their lowest common ancestor (LCA).
Each node will have a reference to its parent node. The definition for Node is below:
```
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node parent;
}
```

According to the definition of LCA on Wikipedia: "The lowest common ancestor of two nodes p and q in a tree T is the lowest node that has both p and q as descendants (where we allow a node to be a descendant of itself)."

Example 1:
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
>
> Output: 3
> Explanation: The LCA of nodes 5 and 1 is 3.

Example 2:
> Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
>
> Output: 5
>
> Explanation: The LCA of nodes 5 and 4 is 5 since a node can be a descendant of itself according to the LCA definition.

> Example 3:
> Input: root = [1,2], p = 1, q = 2
>
> Output: 1

Constraints:
- The number of nodes in the tree is in the range [2, 10<sup>5</sup>]
- -10^<sup>9</sup> <= Node.val <= 10^<sup>9</sup> 
- All Node.val are unique.
- p != q
- p and q exist in the tree.

## Tags
- tree
- linkedlist

## Approach
**Key idea:** Following `parent` pointers turns each node's path to the root into a linked list, so the LCA is the intersection of two linked lists; switching each pointer to the other start when it runs out equalizes the path lengths.

1. Start pointer `a` at `p` and pointer `b` at `q`.
2. Step each pointer to its parent; when a pointer passes the root (becomes `None`), restart it at the other node.
3. After at most `depth(p) + depth(q)` steps both pointers have traveled the same distance and meet at the LCA.
4. Return the node where they meet.

## Code Implementation
```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None
        self.parent = None
"""

class Solution:
    def lowestCommonAncestor(self, p: 'Node', q: 'Node') -> 'Node':
        a, b = p, q
        while a is not b:
            a = a.parent if a else q
            b = b.parent if b else p
        return a
```

## Time Complexity Analysis
> Time complexity  : O(h) — each pointer walks at most the two root paths, where h is the tree height
>
> Space complexity : O(1) — only two pointers

## Related Problems
- [160. Intersection of Two Linked Lists](./160_intersection_of_two_linked_lists.md) — 🟢 Easy · the identical pointer-switching trick
- [236. Lowest Common Ancestor of a Binary Tree](./236_lowest_common_ancestor_of_a_binary_tree.md) — 🟡 Medium · LCA without parent pointers
- [1644. Lowest Common Ancestor of a Binary Tree II](./1644_lowest_common_ancestor_of_a_binary_tree_ii.md) — 🟡 Medium · LCA when p or q may be missing
- [235. Lowest Common Ancestor of a Binary Search Tree](./235_lowest_common_ancestor_of_a_binary_search_tree.md) — 🟡 Medium · LCA using BST ordering
