# 449. Serialize and Deserialize BST

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/serialize-and-deserialize-bst/)

## Question Description
Serialization is converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary search tree. There is no restriction on how your serialization/deserialization algorithm should work. You need to ensure that a binary search tree can be serialized to a string, and this string can be deserialized to the original tree structure.

The encoded string should be as compact as possible.

Example 1:
>
> Input: root = [2,1,3]
>
> Output: [2,1,3]

Example 2:
>
> Input: root = []
>
> Output: []

Constraints:
- The number of nodes in the tree is in the range [0, 10<sup>4</sup> ].
- 0 <= Node.val <= 10<sup>4</sup>
- The input tree is guaranteed to be a binary search tree.

## Tags
- tree

## Approach
**Key idea:** A BST's preorder alone determines its shape, because each value's position follows from the `(lower, upper)` bounds of the BST property — so no null markers are needed.

1. `serialize`: write the preorder values joined by `/` (an empty tree is `""`).
2. `deserialize`: split the string into integers and keep a shared index into them.
3. Build recursively with bounds `(lower, upper)`: if the next value falls outside the bounds, this subtree is empty.
4. Otherwise create the node, advance the index, build the left subtree with bounds `(lower, val)` and the right with `(val, upper)`.

## Code Implementation
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Codec:
    def serialize(self, root: Optional[TreeNode]) -> str:
        """Encodes a tree to a single string (preorder, no null markers)."""
        vals = []

        def preorder(node: Optional[TreeNode]) -> None:
            if node:
                vals.append(str(node.val))
                preorder(node.left)
                preorder(node.right)

        preorder(root)
        return "/".join(vals)

    def deserialize(self, data: str) -> Optional[TreeNode]:
        """Decodes your encoded data to tree."""
        vals = [int(v) for v in data.split("/")] if data else []
        idx = 0

        def build(lower: float, upper: float) -> Optional[TreeNode]:
            nonlocal idx
            if idx == len(vals) or not (lower <= vals[idx] <= upper):
                return None
            val = vals[idx]
            idx += 1
            node = TreeNode(val)
            node.left = build(lower, val)
            node.right = build(val, upper)
            return node

        return build(float('-inf'), float('inf'))


# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# tree = ser.serialize(root)
# ans = deser.deserialize(tree)
# return ans
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node is written and rebuilt once
>
> Space complexity : O(n) — the encoded string and value list (recursion uses O(h))

## Related Problems
- [297. Serialize and Deserialize Binary Tree](./297_serialize_and_deserialize_binary_tree.md) — 🔴 Hard · general tree needs null markers
- [1008. Construct Binary Search Tree from Preorder Traversal](./1008_construct_binary_search_tree_from_preorder_traversal.md) — 🟡 Medium · same bounded preorder rebuild
- [428. Serialize and Deserialize N-ary Tree](./428_serialize_and_deserialize_nary_tree.md) — 🔴 Hard · serialization of a different tree shape
