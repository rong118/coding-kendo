# 450. Delete Node in a BST

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/delete-node-in-a-bst/)

## Question Description
Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.
Basically, the deletion can be divided into two stages:
1. Search for a node to remove.
2. If the node is found, delete the node.

Example 1:
> <img src="https://assets.leetcode.com/uploads/2020/09/04/del_node_1.jpg" width="400" />
>
> Input: root = [5,3,6,2,4,null,7], key = 3
>
> Output: [5,4,6,2,null,null,7]
>
> Explanation: Given key to delete is 3. So we find the node with value 3 and delete it.
> One valid answer is [5,4,6,2,null,null,7], shown in the above BST.
> Please notice that another valid answer is [5,2,6,null,4,null,7] and it's also accepted.
>
> <img src="https://assets.leetcode.com/uploads/2020/09/04/del_node_supp.jpg" width="200" />

Example 2:
> Input: root = [5,3,6,2,4,null,7], key = 0
>
> Output: [5,3,6,2,4,null,7]
>
> Explanation: The tree does not contain a node with value = 0.

Example 3:
> Input: root = [], key = 0
>
> Output: []

Constraints:
- The number of nodes in the tree is in the range [0, 10<sup>4</sup> ].
- -10<sup>5</sup>  <= Node.val <= 10<sup>5</sup> 
- Each node has a unique value.
- root is a valid binary search tree.
- -10<sup>5</sup>  <= key <= 10<sup>5</sup> 

Follow up: Could you solve it with time complexity O(height of tree)?
## Tags
- tree
- bst

## Approach
**Key idea:** Use the BST property to walk to the key; a node with two children can be replaced by its in-order successor (the smallest value in its right subtree), which keeps the tree ordered.

1. If `key` is smaller or larger than `root.val`, recurse into the left or right subtree and reattach the result.
2. When the node is found and it has at most one child, return that child (or `None`) in its place.
3. With two children, find the minimum of the right subtree and copy its value into the node.
4. Recursively delete that successor value from the right subtree.

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
    def deleteNode(self, root: Optional[TreeNode], key: int) -> Optional[TreeNode]:
        if not root:
            return None
        if key < root.val:
            root.left = self.deleteNode(root.left, key)
        elif key > root.val:
            root.right = self.deleteNode(root.right, key)
        else:
            if not root.left:
                return root.right
            if not root.right:
                return root.left
            # Two children: copy the in-order successor, then delete it
            succ = root.right
            while succ.left:
                succ = succ.left
            root.val = succ.val
            root.right = self.deleteNode(root.right, succ.val)
        return root
```

## Time Complexity Analysis
> Time complexity  : O(h) — h = tree height (O(log n) balanced, O(n) worst case)
>
> Space complexity : O(h) — recursion stack

## Related Problems
- [701. Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree) — 🟡 Medium · the matching BST insert operation
- [700. Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree) — 🟢 Easy · the search step of deletion
- [98. Validate Binary Search Tree](./98_validate_binary_search_tree.md) — 🟡 Medium · the BST invariant deletion must preserve
