# 347. Top K Frequent Elements

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
