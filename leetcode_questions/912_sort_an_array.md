# 912. Sort an Array

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/sort-an-array/)

## Question Description
Given an array of integers nums, sort the array in ascending order.

Example 1:
> Input: nums = [5,2,3,1]
> Output: [1,2,3,5]

Example 2:
> Input: nums = [5,1,1,2,0,0]
> Output: [0,0,1,1,2,5]

Constraints:
1 <= nums.length <= 5 * 10<sup>4</sup> 
-5 * 10<sup>4</sup>  <= nums[i] <= 5 * 10<sup>4</sup> 

## Tags
- heap sort

## Approach
**Key idea:** Heap sort — arrange the array into a max-heap in place, then repeatedly swap the maximum to the end and shrink the heap.

1. Build a max-heap by calling `heapify` on every non-leaf index from `n // 2` down to `0`.
2. `heapify` sifts a node down: swap it with its larger child until both children are smaller.
3. For `i` from `n - 1` down to `1`, swap the root (current max) with `nums[i]`, fixing it in its final position.
4. Re-heapify the root over the shrunken heap of size `i`.

## Code Implementation
```python
class Solution:
    def sortArray(self, nums: list[int]) -> list[int]:
        def heapify(arr: list[int], n: int, i: int) -> None:
            largest = i
            left = 2 * i + 1
            right = 2 * i + 2

            if left < n and arr[left] > arr[largest]:
                largest = left
            if right < n and arr[right] > arr[largest]:
                largest = right

            if largest != i:
                arr[i], arr[largest] = arr[largest], arr[i]
                heapify(arr, n, largest)

        n = len(nums)

        for i in range(n // 2, -1, -1):
            heapify(nums, n, i)

        for i in range(n - 1, 0, -1):
            nums[0], nums[i] = nums[i], nums[0]
            heapify(nums, i, 0)

        return nums
```

## Time Complexity Analysis
> Time complexity  : O(n log n)
>
> Space complexity : O(log n) — recursion depth of heapify (sorting itself is in place)

## Related Problems
- [215. Kth Largest Element in an Array](./215_kth_largest_element_in_an_array.md) — 🟡 Medium · heaps / partial sorting
- [75. Sort Colors](./75_sort_colors.md) — 🟡 Medium · in-place sorting with a small value range
- [88. Merge Sorted Array](./88_merge_sorted_array.md) — 🟢 Easy · the merge step of merge sort
