# Array

An array stores elements of the same type in contiguous memory, enabling O(1) random access by index.

## Complexity

| Operation | Time |
|---|---|
| Access | O(1) |
| Insert / Delete at end | O(1) |
| Insert / Delete in middle | O(n) — shifting elements |

## Python Usage

Python's `list` is a dynamic array that grows automatically.

```python
# Create
nums = [10, 20, 30]

# Access & modify
nums[0], nums[-1]    # first & last
nums[1] = 25          # update

# Common operations
nums.sort(); nums.reverse()
max(nums); min(nums); sum(nums)

# Dynamic resizing
nums.append(40)       # O(1) amortized
nums.pop()            # O(1)
nums.remove(20)       # O(n)
```

## Related LeetCode Questions

- [1. Two Sum](../../leetcode_questions/1_two_sum.md)
- [15. 3Sum](../../leetcode_questions/15_three_sum.md)
- [26. Remove Duplicates from Sorted Array](../../leetcode_questions/26_remove_duplicates_from_sorted_array.md)
- [27. Remove Element](../../leetcode_questions/27_remove_element.md)
- [75. Sort Colors](../../leetcode_questions/75_sort_colors.md)
- [169. Majority Element](../../leetcode_questions/169_majority_element.md)
- [217. Contains Duplicate](../../leetcode_questions/217_contain_duplicate.md)
- [238. Product of Array Except Self](../../leetcode_questions/238_product_of_array_except_self.md)
