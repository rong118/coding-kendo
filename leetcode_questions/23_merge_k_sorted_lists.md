# 23. Merge k Sorted Lists

## Question link
(https://leetcode.com/problems/merge-k-sorted-lists/)

## Question Description
You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

Example 1:

> Input: lists = [[1,4,5],[1,3,4],[2,6]]
>
> Output: [1,1,2,3,4,4,5,6]
>
> Explanation: The linked-lists are:
> [
>   1->4->5,
>   1->3->4,
>   2->6
> ]
> merging them into one sorted list:
> 1->1->2->3->4->4->5->6

Example 2:

> Input: lists = []
>
> Output: []

Example 3:

> Input: lists = [[]]
>
> Output: []

Constraints:

* k == lists.length
* 0 <= k <= 10^4
* 0 <= lists[i].length <= 500
* -10^4 <= lists[i][j] <= 10^4
* lists[i] is sorted in **ascending order**.
* The sum of lists[i].length will not exceed 10^4.

## Tags
- linkedlist
- heap

## Code Implementation
```python
import heapq
from typing import Optional

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def mergeKLists(self, lists: list[Optional[ListNode]]) -> Optional[ListNode]:
        dummy = tail = ListNode(0)
        heap = []

        # Push the head of each non-empty list onto the min-heap
        for i, node in enumerate(lists):
            if node:
                heapq.heappush(heap, (node.val, i, node))

        while heap:
            _, i, node = heapq.heappop(heap)
            tail.next = node
            tail = tail.next
            if node.next:
                heapq.heappush(heap, (node.next.val, i, node.next))

        return dummy.next
```

## Time Complexity Analysis
> Time complexity  : O(N log k) — N total nodes across all lists, k lists in the heap
>
> Space complexity : O(k) — the heap holds at most k nodes
