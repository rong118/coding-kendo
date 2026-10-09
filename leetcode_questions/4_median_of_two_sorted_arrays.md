# 4. Median of Two Sorted Arrays

**Difficulty:** 🔴 Hard

## Question link
(https://leetcode.com/problems/median-of-two-sorted-arrays/)

## Question Description
Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.
The overall run time complexity should be O(log (m+n)).

Example 1:
> Input: nums1 = [1,3], nums2 = [2]
>
> Output: 2.00000
>
> Explanation: merged array = [1,2,3] and median is 2.

Example 2:
> Input: nums1 = [1,2], nums2 = [3,4]
>
> Output: 2.50000
> 
> Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
 
Constraints:
* nums1.length == m
* nums2.length == n
* 0 <= m <= 1000
* 0 <= n <= 1000
* 1 <= m + n <= 2000
* -10^6 <= nums1[i], nums2[i] <= 10^6

## Tags
- array
- divide and conque
- binary search

## Approach
**Key idea:** The median is the k-th smallest element of the merged array, and we can find the k-th smallest by comparing the `k/2`-th elements of each array and discarding the `k/2` elements that cannot contain it.

1. Let `total = m + n`; the median is the average of the `(total + 1) // 2`-th and `(total + 2) // 2`-th smallest elements (the same element when `total` is odd).
2. To find the k-th smallest from offsets `a` and `b`: if one array is exhausted, index directly into the other; if `k == 1`, return the smaller head.
3. Otherwise compare `nums1[a + k/2 - 1]` and `nums2[b + k/2 - 1]` (treat out-of-range as infinity).
4. The smaller side's first `k/2` elements are all below the k-th element, so skip them and recurse with `k - k/2`.
5. Each step halves `k`, giving logarithmic time.

## Code Implementation
```python
class Solution:
    def findMedianSortedArrays(self, nums1: list[int], nums2: list[int]) -> float:
        def kth(a: int, b: int, k: int) -> int:
            # k-th smallest (1-indexed) of nums1[a:] + nums2[b:]
            if a == len(nums1):
                return nums2[b + k - 1]
            if b == len(nums2):
                return nums1[a + k - 1]
            if k == 1:
                return min(nums1[a], nums2[b])

            half = k // 2
            a_mid = nums1[a + half - 1] if a + half - 1 < len(nums1) else float("inf")
            b_mid = nums2[b + half - 1] if b + half - 1 < len(nums2) else float("inf")
            if a_mid < b_mid:
                return kth(a + half, b, k - half)
            return kth(a, b + half, k - half)

        total = len(nums1) + len(nums2)
        return (kth(0, 0, (total + 1) // 2) + kth(0, 0, (total + 2) // 2)) / 2
```

## Time Complexity Analysis
> Time complexity  : O(log (m+n))
>
> Space complexity : O(log (m+n)) — recursion depth

## Related Problems
- [23. Merge k Sorted Lists](./23_merge_k_sorted_lists.md) — 🔴 Hard · combining multiple sorted sequences
- [215. Kth Largest Element in an Array](./215_kth_largest_element_in_an_array.md) — 🟡 Medium · k-th order statistic
- [88. Merge Sorted Array](./88_merge_sorted_array.md) — 🟢 Easy · merging two sorted arrays
