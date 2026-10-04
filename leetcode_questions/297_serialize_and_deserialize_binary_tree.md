# 297. Serialize and Deserialize Binary Tree

**Difficulty:** 🔴 Hard

## Question link
(https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)

## Question Description
Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

Clarification: The input/output format is the same as how LeetCode serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

Example 1:
>
> <img src="https://assets.leetcode.com/uploads/2020/09/15/serdeser.jpg" width="400" />
>
> Input: root = [1,2,3,null,null,4,5]
>
> Output: [1,2,3,null,null,4,5]

Example 2:
>
> Input: root = []
>
> Output: []

Example 3:
>
> Input: root = [1]
>
> Output: [1]

Example 4:
>
> Input: root = [1,2]
>
> Output: [1,2]


Constraints:
- The number of nodes in the tree is in the range [0, 10n<sup>4</sup> ].
- -1000 <= Node.val <= 1000

## Tags
- tree

## Approach
**Key idea:** A preorder traversal that also writes a marker (`#`) for every missing child describes the tree exactly, so it can be read back in the same order without ambiguity.

1. `serialize`: do a preorder DFS, writing the node value, or `#` for `None`.
2. Join the tokens with a delimiter (`,`).
3. `deserialize`: split the string into tokens and read them through an iterator.
4. Read the next token: `#` means `None`; otherwise create a node, then build its left subtree, then its right subtree.

## Code Implementation
```python
from typing import Optional

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:
    def serialize(self, root: Optional[TreeNode]) -> str:
        out = []

        def dfs(node: Optional[TreeNode]) -> None:
            if node is None:
                out.append('#')
                return
            out.append(str(node.val))
            dfs(node.left)
            dfs(node.right)

        dfs(root)
        return ','.join(out)

    def deserialize(self, data: str) -> Optional[TreeNode]:
        tokens = iter(data.split(','))

        def build() -> Optional[TreeNode]:
            tok = next(tokens)
            if tok == '#':
                return None
            node = TreeNode(int(tok))
            node.left = build()
            node.right = build()
            return node

        return build()

# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node is serialized and rebuilt once
>
> Space complexity : O(n) — the string/token list plus the recursion stack

## Related Problems
- [449. Serialize and Deserialize BST](./449_serialize_and_deserialize_BST.md) — 🟡 Medium · BST ordering lets you drop the null markers
- [428. Serialize and Deserialize N-ary Tree](./428_serialize_and_deserialize_nary_tree.md) — 🔴 Hard · same idea with a child count per node
- [105. Construct Binary Tree from Preorder and Inorder Traversal](./105_construct_binary_tree_from_preorder_and_inorder_traversal.md) — 🟡 Medium · rebuilding a tree from a traversal
