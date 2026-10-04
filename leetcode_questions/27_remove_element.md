# 27. Remove Element

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/remove-element/)

## Question Description
Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The relative order of the elements may be changed.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

Example 1:

> Input: nums = [3,2,2,3], val = 3
> 
> Output: 2, nums = [2,2,_,_]
>
> Explanation: Your function should return k = 2, with the first two elements of nums being 2.
>
> It does not matter what you leave beyond the returned k (hence they are underscores).

Example 2:

> Input: nums = [0,1,2,2,3,0,4,2], val = 2
>
> Output: 5, nums = [0,1,4,0,3,_,_,_]
>
> Explanation: Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4.
>
> Note that the five elements can be returned in any order.
>
> It does not matter what you leave beyond the returned k (hence they are underscores).

Constraints:

- 0 <= nums.length <= 100
- 0 <= nums[i] <= 50
- 0 <= val <= 100

## Tags
- array
- two pointers


## Approach
**Key idea:** Use a slow write pointer and a fast read pointer — every element that isn't `val` is copied forward, so the first `i` slots end up holding exactly the kept elements.

1. Set the write index `i = 0`.
2. Scan every index `j` with the read pointer.
3. If `A[j] != val`, copy it to `A[i]` and advance `i`.
4. Return `i`, the count of kept elements.

## Code Implementation
```python
def removeElement(A, val):
    i = 0
    for j in range(len(A)):
        if A[j] != val:
            A[i] = A[j]
            i += 1

    return i
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1)

## Related Problems
- [26. Remove Duplicates from Sorted Array](./26_remove_duplicates_from_sorted_array.md) — 🟢 Easy · same slow/fast in-place compaction
- [283. Move Zeroes](https://leetcode.com/problems/move-zeroes) — 🟢 Easy · in-place compaction keeping non-target elements
- [75. Sort Colors](./75_sort_colors.md) — 🟡 Medium · in-place partitioning with pointers
