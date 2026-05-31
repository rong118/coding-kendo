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

| # | Problem | Difficulty | Technique |
|---|---------|------------|-----------|
| 26 | [Remove Duplicates from Sorted Array](../../leetcode_questions/26_remove_duplicates_from_sorted_array.md) | Easy | In-place overwrite with write pointer |
| 48 | [Rotate Image](../../leetcode_questions/48_rotate_image.md) | Medium | 2D transpose + reverse |
| 88 | [Merge Sorted Array](../../leetcode_questions/88_merge_sorted_array.md) | Easy | Fill from end |
| 189 | [Rotate Array](../../leetcode_questions/189_rotate_array.md) | Medium | Three-reversal in-place rotation |
| 448 | [Find All Numbers Disappeared in an Array](../../leetcode_questions/448_find_all_numbers_disappeared_in_an_array.md) | Easy | Values as indices / in-place marking |
