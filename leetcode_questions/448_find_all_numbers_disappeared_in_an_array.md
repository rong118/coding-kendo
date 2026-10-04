# 448. Find All Numbers Disappeared in an Array

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)

## Question Description
Given an array `nums` of `n` integers where `nums[i]` is in the range `[1, n]`, return an array of all the integers in the range `[1, n]` that do not appear in `nums`.

Example 1:

> Input: nums = [4,3,2,7,8,2,3,1]
>
> Output: [5,6]

Example 2:

> Input: nums = [1,1]
>
> Output: [2]

Constraints:

- n == nums.length
- 1 <= n <= 10⁵
- 1 <= nums[i] <= n

## Tags
- array
- in-place

## Approach
**Key idea:** Values are in `[1, n]`, so each value can mark its own index `value - 1` by making that slot negative; indices that stay positive were never seen.

1. For each number `n`, compute `idx = abs(n) - 1` (use `abs` since it may already be negated).
2. Set `nums[idx]` to negative to mark `idx + 1` as present.
3. Scan the array again; every index `i` with `nums[i] > 0` means `i + 1` is missing.
4. Return those missing values.

## Code Implementation
```python
def findDisappearedNumbers(nums):
    # mark seen values by negating the value at their index
    for n in nums:
        idx = abs(n) - 1
        nums[idx] = -abs(nums[idx])

    # collect indices that remain positive
    result = []
    for i, n in enumerate(nums):
        if n > 0:
            result.append(i + 1)

    return result
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1) — output array not counted as extra space

## Related Problems
- [287. Find the Duplicate Number](./287_find_the_duplicate_number.md) — 🟡 Medium · values in `[1, n]` used as indices
- [442. Find All Duplicates in an Array](https://leetcode.com/problems/find-all-duplicates-in-an-array) — 🟡 Medium · same negation-marking trick
- [41. First Missing Positive](https://leetcode.com/problems/first-missing-positive) — 🔴 Hard · in-place index marking to find a missing value
- [268. Missing Number](https://leetcode.com/problems/missing-number) — 🟢 Easy · finding a missing value in `[0, n]`
