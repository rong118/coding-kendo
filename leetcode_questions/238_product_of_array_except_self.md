# 238. Product of Array Except Self

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/product-of-array-except-self/description/)

## Question Description
Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.

Example 1:

> Input: nums = [1,2,3,4]
>
> Output: [24,12,8,6]

Example 2:

> Input: nums = [-1,1,0,-3,3]
>
> Output: [0,0,9,0,0]

Constraints:
- 2 <= nums.length <= 105
- -30 <= nums[i] <= 30
- The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

Follow up: Can you solve the problem in O(1) extra space complexity? (The output array does not count as extra space for space complexity analysis.)

## Tags
- array
- prefix

## Approach
**Key idea:** `answer[i]` is (product of everything left of `i`) × (product of everything right of `i`), so two passes of running products give the answer without division.

1. Fill `result[i]` with the product of all elements to the left of `i` (prefix products, `result[0] = 1`).
2. Walk from the right keeping a running product `right` of elements to the right of `i`.
3. Multiply `result[i]` by `right`, then fold `nums[i]` into `right`.
4. Only one extra variable is used besides the output array.

## Code Implementation
```python
def productExceptSelf(nums):
    n = len(nums)
    result = [1] * n

    # Left pass: product of all elements to the left of i
    for i in range(1, n):
        result[i] = result[i - 1] * nums[i - 1]

    # Right pass: product of all elements to the right of i
    right = 1
    for i in reversed(range(n)):
        result[i] *= right
        right *= nums[i]

    return result
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1) — extra space, excluding the output array

## Related Problems
- [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water) — 🔴 Hard · combine left and right prefix passes
- [152. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray) — 🟡 Medium · running products over an array
- [724. Find Pivot Index](https://leetcode.com/problems/find-pivot-index) — 🟢 Easy · prefix vs. suffix aggregates
