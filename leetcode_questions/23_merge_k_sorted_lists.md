# 23. Merge k Sorted Lists

**Difficulty:** 🔴 Hard

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

## Approach
**Key idea:** The next node of the merged list is always the smallest of the k current heads, so keep those heads in a min-heap and repeatedly pop the minimum.

1. Push the head of every non-empty list onto a min-heap as `(val, list_index, node)`; the index breaks ties so nodes are never compared.
2. Pop the smallest node and append it to the tail of the result (built from a dummy head).
3. If the popped node has a `next`, push that node onto the heap.
4. Repeat until the heap is empty, then return `dummy.next`.

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

## Related Problems
- [21. Merge Two Sorted Lists](./21_merge_two_sorted_lists.md) — 🟢 Easy · the k = 2 case
- [88. Merge Sorted Array](./88_merge_sorted_array.md) — 🟢 Easy · merging sorted sequences
- [215. Kth Largest Element in an Array](./215_kth_largest_element_in_an_array.md) — 🟡 Medium · heap of bounded size
