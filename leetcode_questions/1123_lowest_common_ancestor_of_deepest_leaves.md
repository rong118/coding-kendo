# 1123. Lowest Common Ancestor of Deepest Leaves

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/lowest-common-ancestor-of-deepest-leaves/)

## Question Description
Given the root of a binary tree, return the lowest common ancestor of its deepest leaves.

Recall that:
The node of a binary tree is a leaf if and only if it has no children
The depth of the root of the tree is 0. if the depth of a node is d, the depth of each of its children is d + 1.
The lowest common ancestor of a set S of nodes, is the node A with the largest depth such that every node in S is in the subtree with root A.
 
Example 1:
> <img src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/01/sketch1.png" width="400" />
>
> Input: root = [3,5,1,6,2,0,8,null,null,7,4]
>
> Output: [2,7,4]
>
> Explanation: We return the node with value 2, colored in yellow in the diagram.
>
> The nodes coloured in blue are the deepest leaf-nodes of the tree.
>
> Note that nodes 6, 0, and 8 are also leaf nodes, but the depth of them is 2, but the depth of nodes 7 and 4 is 3.

Example 2:
> Input: root = [1]
>
> Output: [1]
>
> Explanation: The root is the deepest node in the tree, and it's the lca of itself.

Example 3:
> Input: root = [0,1,3,null,2]
>
> Output: [2]
>
> Explanation: The deepest leaf node in the tree is 2, the lca of one node is itself.
 

Constraints:
- The number of nodes in the tree will be in the range [1, 1000].
- 0 <= Node.val <= 1000
- The values of the nodes in the tree are unique.
 

Note: This question is the same as 865: https://leetcode.com/problems/smallest-subtree-with-all-the-deepest-nodes/

<br/>

## Tags
- tree
- dfs


## Approach
**Key idea:** A node is the answer exactly when its left and right subtrees reach the same maximum depth; otherwise the answer lies in the deeper subtree.

1. Approach 1 (top-down): compute the heights of the left and right subtrees; if equal return the node, else recurse into the taller side. Heights are recomputed at every level, so it is O(n²) in the worst case.
2. Approach 2 (bottom-up): a post-order DFS returns a pair `(lca, depth)` for each subtree, where `depth` is the deepest level reached.
3. For a null child return `(None, depth)`; for a node, get the pairs from both children.
4. If both depths are equal, this node is the LCA of the deepest leaves: return `(node, depth)`. Otherwise pass up the pair from the deeper side.

## Code Implementation
### Approach 1: Compare subtree heights — O(n²)
```python
from typing import Optional

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def lcaDeepestLeaves(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
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

### Approach 2: Post-order DFS returning (lca, depth) — O(n)
```python
from typing import Optional

class Solution:
    def lcaDeepestLeaves(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        def dfs(node: Optional[TreeNode], d: int) -> tuple[Optional[TreeNode], int]:
            if not node:
                return None, d
            l_node, l_depth = dfs(node.left, d + 1)
            r_node, r_depth = dfs(node.right, d + 1)
            if l_depth == r_depth:
                return node, l_depth
            return (l_node, l_depth) if l_depth > r_depth else (r_node, r_depth)

        return dfs(root, 0)[0]
```

## Time Complexity Analysis
> Time complexity  : O(n) for Approach 2 (each node visited once); Approach 1 is O(n · h), O(n²) worst case
>
> Space complexity : O(h) — recursion stack, O(n) worst case for a skewed tree

## Related Problems
- [865. Smallest Subtree with all the Deepest Nodes](./865_smallest_subtree_with_all_the_deepest_nodes.md) — 🟡 Medium · identical problem
- [236. Lowest Common Ancestor of a Binary Tree](./236_lowest_common_ancestor_of_a_binary_tree.md) — 🟡 Medium · classic LCA via post-order recursion
- [1644. Lowest Common Ancestor of a Binary Tree II](./1644_lowest_common_ancestor_of_a_binary_tree_ii.md) — 🟡 Medium · LCA variant returning extra info from DFS
- [1676. Lowest Common Ancestor of a Binary Tree IV](./1676_lowest_common_ancestor_of_a_binary_tree_iv.md) — 🟡 Medium · LCA of a set of nodes
