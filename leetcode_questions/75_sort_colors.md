# 75. Sort Colors

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/sort-colors/)

## Question Description
Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.

Example 1:

> Input: nums = [2,0,2,1,1,0]
> 
> Output: [0,0,1,1,2,2]

Example 2:

> Input: nums = [2,0,1]
>
> Output: [0,1,2]
 
Constraints:
- n == nums.length
- 1 <= n <= 300
- nums[i] is either 0, 1, or 2.

## Tags
- Array
- Sort

## Approach
**Key idea:** Dutch National Flag partitioning — keep `[0, low)` all 0s, `[low, mid)` all 1s and `(high, n-1]` all 2s, shrinking the unknown window `[mid, high]` in one pass.

1. Start with `low = mid = 0` and `high = n - 1`.
2. If `nums[mid]` is 0, swap it with `nums[low]` and advance both `low` and `mid`.
3. If it is 1, it's already in the right region — just advance `mid`.
4. If it is 2, swap it with `nums[high]` and decrement `high` (don't advance `mid`; the swapped-in value is still unchecked).
5. Stop when `mid > high`.

## Code Implementation
```python
# Dutch National Flag problem
def sortColors(nums):
    low, mid, high = 0, 0, len(nums) - 1

    while mid <= high:
        if nums[mid] == 0:
            nums[low], nums[mid] = nums[mid], nums[low]
            low += 1
            mid += 1
        elif nums[mid] == 1:
            mid += 1
        else:  # nums[mid] == 2
            nums[mid], nums[high] = nums[high], nums[mid]
            high -= 1
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1)

## Related Problems
- [912. Sort an Array](./912_sort_an_array.md) — 🟡 Medium · general sorting; quicksort uses the same partition idea
- [27. Remove Element](./27_remove_element.md) — 🟢 Easy · in-place partitioning with pointers
- [215. Kth Largest Element in an Array](./215_kth_largest_element_in_an_array.md) — 🟡 Medium · quickselect relies on in-place partitioning
