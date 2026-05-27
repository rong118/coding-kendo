# 448. Find All Numbers Disappeared in an Array

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
