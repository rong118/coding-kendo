# 347. Top K Frequent Elements

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/top-k-frequent-elements/)

## Question Description
Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

Example 1:

> Input: nums = [1,1,1,2,2,3], k = 2
> Output: [1,2]

Example 2:

> Input: nums = [1], k = 1
> Output: [1]


Constraints:

1 <= nums.length <= 10<sup>5</sup>
k is in the range [1, the number of unique elements in the array].
It is guaranteed that the answer is unique.

## Tags
- heap

## Approach
**Key idea:** Count frequencies, then keep a min-heap of size `k` keyed by frequency — anything smaller than the heap's minimum can never be in the top `k`.

1. Count each number's frequency with a `Counter`.
2. Push `(freq, num)` pairs onto a min-heap.
3. Whenever the heap grows past `k`, pop the least frequent pair.
4. The `k` pairs left in the heap are the answer.

## Code Implementation
```python
import heapq
from collections import Counter

class Solution:
    def topKFrequent(self, nums: list[int], k: int) -> list[int]:
        count = Counter(nums)
        heap = []

        for num, freq in count.items():
            heapq.heappush(heap, (freq, num))
            if len(heap) > k:
                heapq.heappop(heap)

        return [num for _, num in heap]
```

## Time Complexity Analysis
> Time complexity  : O(n log k)
>
> Space complexity : O(n)

## Related Problems
- [215. Kth Largest Element in an Array](./215_kth_largest_element_in_an_array.md) — 🟡 Medium · size-k min-heap
- [703. Kth Largest Element in a Stream](./703_kth_largest_element_in_a_stream.md) — 🟢 Easy · size-k min-heap
- [692. Top K Frequent Words](https://leetcode.com/problems/top-k-frequent-words) — 🟡 Medium · same problem with tie-breaking
- [451. Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency) — 🟡 Medium · frequency counting and ordering
