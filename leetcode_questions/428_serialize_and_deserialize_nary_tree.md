# 428. Serialize and Deserialize N-ary Tree

**Difficulty:** 🔴 Hard

## Question link
(https://leetcode.com/problems/serialize-and-deserialize-n-ary-tree/)

## Question Description
Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize an N-ary tree. An N-ary tree is a rooted tree in which each node has no more than N children. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that an N-ary tree can be serialized to a string and this string can be deserialized to the original tree structure.


For example, you may serialize the following 3-ary tree:

as [1 [3[5 6] 2 4]]. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

Note:
N is in the range of [1, 1000].
Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.

List
- N is in the range of [1, 1000].
- Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.

## Tags
- tree

## Approach
**Key idea:** Write each node in preorder as its value followed by its number of children. When reading back, the count tells you exactly how many subtrees to build under each node, so no brackets or null markers are needed.

1. `serialize`: preorder DFS; for each node append `val` and `len(children)`, then serialize each child.
2. Join the tokens with spaces (an empty tree becomes an empty string).
3. `deserialize`: split into tokens and read them through a local iterator, so the codec keeps no state between calls.
4. Read a value and a child count, create the node, then build that many children recursively, in order.

## Code Implementation
```python
from typing import Optional

# Definition for a Node.
# class Node:
#     def __init__(self, val: Optional[int] = None, children: Optional[list['Node']] = None):
#         self.val = val
#         self.children = children if children is not None else []

class Codec:
    def serialize(self, root: 'Node') -> str:
        # Preorder: each node is written as "val childCount"
        out = []

        def dfs(node: 'Node') -> None:
            out.append(str(node.val))
            out.append(str(len(node.children)))
            for child in node.children:
                dfs(child)

        if root:
            dfs(root)
        return ' '.join(out)

    def deserialize(self, data: str) -> 'Node':
        if not data:
            return None
        tokens = iter(data.split())

        def build() -> 'Node':
            node = Node(int(next(tokens)))
            for _ in range(int(next(tokens))):
                node.children.append(build())
            return node

        return build()
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node is written and read once
>
> Space complexity : O(n) — the token list plus the recursion stack

## Related Problems
- [297. Serialize and Deserialize Binary Tree](./297_serialize_and_deserialize_binary_tree.md) — 🔴 Hard · binary-tree version with null markers
- [449. Serialize and Deserialize BST](./449_serialize_and_deserialize_BST.md) — 🟡 Medium · compact encoding using tree structure
- [589. N-ary Tree Preorder Traversal](https://leetcode.com/problems/n-ary-tree-preorder-traversal) — 🟢 Easy · the preorder traversal used here
