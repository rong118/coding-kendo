# 99. Recover Binary Search Tree

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/recover-binary-search-tree/)

## Question Description
You are given the root of a binary search tree (BST), where the values of exactly two nodes of the tree were swapped by mistake. Recover the tree without changing its structure.

<br/>
Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/10/28/recover1.jpg" width="400" />
>
> Input: root = [1,3,null,null,2]
>
> Output: [3,1,null,null,2]
>
> Explanation: 3 cannot be a left child of 1 because 3 > 1. Swapping 1 and 3 makes the BST valid.

Example 2:
> <img src="https://assets.leetcode.com/uploads/2020/10/28/recover2.jpg" width="400" />
>
> Input: root = [3,1,4,null,null,2]
>
> Output: [2,1,4,null,null,3]
>
> Explanation: 2 cannot be in the right subtree of 3 because 2 < 3. Swapping 2 and 3 makes the BST valid.


Constraints:
- The number of nodes in the tree is in the range [2, 1000].
- -2<sup>31</sup> <= Node.val <= 2<sup>31</sup> - 1

Follow up: A solution using O(n) space is pretty straight-forward. Could you devise a constant O(1) space solution?

## Tags
- tree
- bst

## Approach
**Key idea:** An in-order traversal of a BST is sorted, so swapping two nodes creates one or two "drops" (`prev.val > cur.val`); the first misplaced node is the `prev` of the first drop and the second is the `cur` of the last drop.

1. Traverse the tree in order, remembering the previously visited node.
2. At the first drop, record `prev` as `first`.
3. At every drop, record the current node as `second` (handles both adjacent and distant swaps).
4. After the traversal, swap the values of `first` and `second`.
5. Approach 2 does the same scan over an explicit list of in-order nodes, trading O(n) space for simplicity.

## Code Implementation
### Approach 1: In-order with previous pointer

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

from typing import Optional


class Solution:
    def recoverTree(self, root: Optional[TreeNode]) -> None:
        """Do not return anything, modify root in-place instead."""
        self.prev: Optional[TreeNode] = None
        self.first: Optional[TreeNode] = None
        self.second: Optional[TreeNode] = None

        def inorder(node: Optional[TreeNode]) -> None:
            if not node:
                return
            inorder(node.left)
            if self.prev and self.prev.val > node.val:
                if not self.first:
                    self.first = self.prev  # first inversion: the larger value
                self.second = node          # last inversion: the smaller value
            self.prev = node
            inorder(node.right)

        inorder(root)
        if self.first and self.second:
            self.first.val, self.second.val = self.second.val, self.first.val
```

### Approach 2: In-order list

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

from typing import Optional


class Solution:
    def recoverTree(self, root: Optional[TreeNode]) -> None:
        """Do not return anything, modify root in-place instead."""
        nodes: list[TreeNode] = []

        def inorder(node: Optional[TreeNode]) -> None:
            if not node:
                return
            inorder(node.left)
            nodes.append(node)
            inorder(node.right)

        inorder(root)
        first = last = -1
        for i in range(len(nodes) - 1):
            if nodes[i].val > nodes[i + 1].val:
                if first == -1:
                    first = i
                last = i + 1
        if first != -1:
            nodes[first].val, nodes[last].val = nodes[last].val, nodes[first].val
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(h) for Approach 1 (recursion stack, h = tree height); O(n) for Approach 2 (list of nodes)

## Related Problems
- [98. Validate Binary Search Tree](./98_validate_binary_search_tree.md) — 🟡 Medium · same in-order "previous value" check
- [94. Binary Tree Inorder Traversal](./94_binary_tree_inorder_traversal.md) — 🟢 Easy · the traversal this solution is built on
- [173. Binary Search Tree Iterator](./173_binary_search_tree_iterator.md) — 🟡 Medium · in-order traversal of a BST yields sorted order
