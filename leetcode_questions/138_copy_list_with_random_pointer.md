# 138. Copy List with Random Pointer

## Question link
(https://leetcode.com/problems/copy-list-with-random-pointer/)

## Question Description
A linked list of length `n` is given such that each node contains an additional random pointer, which could point to any node in the list, or `null`.

Construct a **deep copy** of the list. The deep copy should consist of exactly `n` brand new nodes, where each new node has its value set to the value of its corresponding original node. Both the `next` and `random` pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. **None** of the pointers in the new list should point to nodes in the original list.

Return the head of the copied linked list.

Example 1:

> Input: head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
>
> Output: [[7,null],[13,0],[11,4],[10,2],[1,0]]

Example 2:

> Input: head = [[1,1],[2,1]]
>
> Output: [[1,1],[2,1]]

Example 3:

> Input: head = [[3,null],[3,0],[3,null]]
>
> Output: [[3,null],[3,0],[3,null]]

Constraints:

* 0 <= n <= 1000
* -10^4 <= Node.val <= 10^4
* Node.random is `null` or is pointing to some node in the linked list.

## Tags
- linkedlist

## Code Implementation
```python
from typing import Optional

class Node:
    def __init__(self, x: int, next: 'Optional[Node]' = None, random: 'Optional[Node]' = None):
        self.val = int(x)
        self.next = next
        self.random = random

class Solution:
    # Hash map approach — two pass, O(n) space
    def copyRandomList(self, head: Optional[Node]) -> Optional[Node]:
        if not head:
            return None

        old_to_new = {}

        # First pass: clone nodes and build mapping
        cur = head
        while cur:
            old_to_new[cur] = Node(cur.val)
            cur = cur.next

        # Second pass: wire next and random pointers
        cur = head
        while cur:
            if cur.next:
                old_to_new[cur].next = old_to_new[cur.next]
            if cur.random:
                old_to_new[cur].random = old_to_new[cur.random]
            cur = cur.next

        return old_to_new[head]

    # Interweaving approach — three pass, O(1) extra space
    def copyRandomListO1(self, head: Optional[Node]) -> Optional[Node]:
        if not head:
            return None

        # 1. Insert copy nodes interleaved: A → A' → B → B'
        cur = head
        while cur:
            copy = Node(cur.val, cur.next)
            cur.next = copy
            cur = copy.next

        # 2. Wire random pointers of the copies
        cur = head
        while cur:
            if cur.random:
                cur.next.random = cur.random.next
            cur = cur.next.next

        # 3. Separate the two lists
        cur = head
        copy_head = head.next
        while cur:
            copy = cur.next
            cur.next = copy.next
            if copy.next:
                copy.next = copy.next.next
            cur = cur.next

        return copy_head
```

## Time Complexity Analysis
> Time complexity  : O(n) — each approach visits every node a constant number of times
>
> Space complexity : O(n) hash map approach; O(1) interweaving approach
