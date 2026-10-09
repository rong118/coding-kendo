# 215. Kth Largest Element in an Array

**Difficulty:** 🟡 Medium

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

## Approach
**Key idea:** A min-heap capped at size `k` always holds the `k` largest values seen so far, and its smallest element (the root) is the `k`th largest.

1. Create an empty min-heap.
2. Push each number onto the heap.
3. Whenever the heap grows past `k` elements, pop the smallest.
4. After processing all numbers, return the heap root.

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

## Related Problems
- [703. Kth Largest Element in a Stream](./703_kth_largest_element_in_a_stream.md) — 🟢 Easy · same size-k min-heap on a stream
- [347. Top K Frequent Elements](./347_top_k_frequent_elements.md) — 🟡 Medium · size-k heap over frequencies
- [973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin) — 🟡 Medium · top-k selection with a heap
- [912. Sort an Array](./912_sort_an_array.md) — 🟡 Medium · quicksort partitioning behind quickselect
