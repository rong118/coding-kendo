# 426. Convert Binary Search Tree to Sorted Doubly Linked List

## Question link
(https://leetcode.com/problems/convert-binary-search-tree-to-sorted-doubly-linked-list/)

## Question Description
Convert a **Binary Search Tree** to a sorted **Circular Doubly-Linked List** in place.

You can think of the left and right pointers as synonymous to the predecessor and successor pointers in a doubly-linked list. For a circular doubly linked list, the predecessor of the first element is the last element, and the successor of the last element is the first element.

We want to do the transformation **in place**. After the transformation, the `left` pointer of the tree node should point to its predecessor, and the `right` pointer should point to its successor. You should return the pointer to the smallest element of the linked list.

Example 1:

> Input: root = [4,2,5,1,3]
>
> Output: [1,2,3,4,5]

Example 2:

> Input: root = [2,1,3]
>
> Output: [1,2,3]

Constraints:

* The number of nodes in the tree is in the range [0, 2000].
* -1000 <= Node.val <= 1000

## Tags
- linkedlist
- tree

## Code Implementation
```python
from typing import Optional

class Node:
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def treeToDoublyList(self, root: Optional[Node]) -> Optional[Node]:
        if not root:
            return None

        head = None
        prev = None

        # In-order traversal wires left/right as prev/next
        def inorder(node: Node) -> None:
            nonlocal head, prev
            if not node:
                return

            inorder(node.left)

            if not head:
                head = node
            if prev:
                prev.right = node
                node.left = prev
            prev = node

            inorder(node.right)

        inorder(root)

        # Close the circular links
        head.left = prev
        prev.right = head

        return head
```

## Time Complexity Analysis
> Time complexity  : O(n) — each node visited once via in-order traversal
>
> Space complexity : O(h) — recursion stack, where h is the tree height
