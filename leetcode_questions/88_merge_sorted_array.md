# 88. Merge Sorted Array

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/merge-sorted-array/)

## Question Description
You are given two integer arrays `nums1` and `nums2`, sorted in non-decreasing order, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.

Merge nums1 and nums2 into a single array sorted in non-decreasing order.

The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.

Example 1:

> Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
>
> Output: [1,2,2,3,5,6]
>
> Explanation: The arrays we are merging are [1,2,3] and [2,5,6]. The result of the merge is [1,2,2,3,5,6].

Example 2:

> Input: nums1 = [1], m = 1, nums2 = [], n = 0
>
> Output: [1]
>
> Explanation: The arrays we are merging are [1] and []. The result of the merge is [1].

Example 3:

> Input: nums1 = [0], m = 0, nums2 = [1], n = 1
>
> Output: [1]
>
> Explanation: The arrays we are merging are [] and [1]. The result of the merge is [1].

Constraints:

- nums1.length == m + n
- nums2.length == n
- 0 <= m, n <= 200
- 1 <= m + n <= 200
- -10⁹ <= nums1[i], nums2[j] <= 10⁹

## Tags
- array
- two pointers

## Approach
**Key idea:** The free space is at the end of `nums1`, so filling it from the back with the largest remaining value never overwrites an element that hasn't been merged yet.

1. Set `i = m - 1`, `j = n - 1` (last real elements) and `k = m + n - 1` (last slot).
2. While `nums2` still has elements, copy the larger of `nums1[i]` and `nums2[j]` into `nums1[k]`.
3. Move back the pointer you copied from, and move `k` back.
4. Once `nums2` is used up, anything left in `nums1` is already in place.

## Code Implementation
```python
def merge(nums1, m, nums2, n):
    # fill from the end
    i, j, k = m - 1, n - 1, m + n - 1

    while j >= 0:
        if i >= 0 and nums1[i] > nums2[j]:
            nums1[k] = nums1[i]
            i -= 1
        else:
            nums1[k] = nums2[j]
            j -= 1
        k -= 1
```

## Time Complexity Analysis
> Time complexity  : O(m + n)
>
> Space complexity : O(1)

## Related Problems
- [21. Merge Two Sorted Lists](./21_merge_two_sorted_lists.md) — 🟢 Easy · same merge step on linked lists
- [977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array) — 🟢 Easy · two pointers filling the output from the back
- [4. Median of Two Sorted Arrays](./4_median_of_two_sorted_arrays.md) — 🔴 Hard · combines two sorted arrays
