# 215. Kth Largest Element in an Array

## Question link
(https://leetcode.com/problems/kth-largest-element-in-an-array/)

## Question Description
Given an integer array `nums` and an integer `k`, return the `kth` largest element in the array.

Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Example 1:

> Input: nums = [3,2,1,5,6,4], k = 2
>
> Output: 5

Example 2:

> Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
>
> Output: 4

Constraints:

* 1 <= k <= nums.length <= 10^4
* -10^4 <= nums[i] <= 10^4

## Tags
- heap

## Code Implementation
```python
import heapq

class Solution:
    def findKthLargest(self, nums: list[int], k: int) -> int:
        # Maintain a min-heap of size k containing the k largest elements seen so far
        heap = []
        for num in nums:
            heapq.heappush(heap, num)
            if len(heap) > k:
                heapq.heappop(heap)  # evict the smallest among the k+1

        # The root of the min-heap is the kth largest overall
        return heap[0]
```

## Time Complexity Analysis
> Time complexity  : O(n log k) — each push/pop on a heap of size ≤ k is O(log k)
>
> Space complexity : O(k) — the heap holds at most k elements
