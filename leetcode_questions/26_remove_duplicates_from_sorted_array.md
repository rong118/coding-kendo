# 26. Remove Duplicates from Sorted Array

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

## Question Description
Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.

Return k after placing the final result in the first k slots of nums.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

Custom Judge:

The judge will test your solution with the following code:

int[] nums = [...]; // Input array
int[] expectedNums = [...]; // The expected answer with correct length

int k = removeDuplicates(nums); // Calls your implementation

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
If all assertions pass, then your solution will be accepted.

Example 1:

> Input: nums = [1,1,2]
>
> Output: 2, nums = [1,2,_]
> Explanation: Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
>
> It does not matter what you leave beyond the returned k (hence they are underscores).

Example 2:

> Input: nums = [0,0,1,1,1,2,2,3,3,4]
>
> Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]
> 
> Explanation: Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
>
> It does not matter what you leave beyond the returned k (hence they are underscores).
 

Constraints:

- 1 <= nums.length <= 3 * 10^4
- -100 <= nums[i] <= 100
- nums is sorted in non-decreasing order.

## Tags
- array
- two pointers

## Approach
**Key idea:** Because the array is sorted, duplicates are adjacent, so a slow pointer can mark the end of the unique prefix while a fast pointer scans for the next new value.

1. Let `i` point at the last unique element written (start at index 0).
2. Scan `j` from index 1 to the end.
3. When `nums[j]` differs from `nums[i]`, advance `i` and copy `nums[j]` into `nums[i]`.
4. Return `i + 1`, the length of the unique prefix.

## Code Implementation
```python
def removeDuplicates(nums):
    if not nums:
        return 0

    i = 0  # pointer for the last unique element
    for j in range(1, len(nums)):
        if nums[j] != nums[i]:
            i += 1
            nums[i] = nums[j]
    
    return i + 1
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1)

## Related Problems
- [27. Remove Element](./27_remove_element.md) — 🟢 Easy · same slow/fast in-place overwrite
- [80. Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii) — 🟡 Medium · allow each value up to twice
- [83. Remove Duplicates from Sorted List](./83_remove_duplicates_from_sorted_list.md) — 🟢 Easy · same idea on a linked list
- [88. Merge Sorted Array](./88_merge_sorted_array.md) — 🟢 Easy · in-place two-pointer array writing
