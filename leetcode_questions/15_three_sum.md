# 15. 3Sum

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/3sum/)

## Question Description
Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

Example 1:

> Input: nums = [-1,0,1,2,-1,-4]
>
> Output: [[-1,-1,2],[-1,0,1]]
>
> Explanation: 
> nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
>
> nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
>
> nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
>
> The distinct triplets are [-1,0,1] and [-1,-1,2].
>
> Notice that the order of the output and the order of the triplets does not matter.

Example 2:

> Input: nums = [0,1,1]
>
> Output: []
>
> Explanation: The only possible triplet does not sum up to 0.

Example 3:

> Input: nums = [0,0,0]
>
> Output: [[0,0,0]]
>
> Explanation: The only possible triplet sums up to 0.
 

Constraints:

* 3 <= nums.length <= 3000
* -10^5 <= nums[i] <= 10^5

## Tags
- array
- two pointers

## Approach
**Key idea:** After sorting, fixing the first number turns the problem into a sorted Two Sum, which two pointers solve in linear time; skipping equal neighbours removes duplicate triplets.

1. Sort `nums`.
2. For each index `i`, skip it if `nums[i]` equals the previous value (same first number already tried).
3. Set `left = i + 1`, `right = n - 1` and look at `nums[i] + nums[left] + nums[right]`.
4. If the sum is too small move `left` right; if too large move `right` left.
5. On a zero sum, record the triplet, skip over equal values on both sides, then move both pointers inward.

## Code Implementation
```python
def threeSum(nums):
    nums.sort()
    result = []
    n = len(nums)

    for i in range(n - 2):
        # Skip duplicate values for the first number
        if i > 0 and nums[i] == nums[i - 1]:
            continue

        left, right = i + 1, n - 1

        while left < right:
            total = nums[i] + nums[left] + nums[right]

            if total < 0:
                left += 1
            elif total > 0:
                right -= 1
            else:
                # Found a valid triplet
                result.append([nums[i], nums[left], nums[right]])

                # Skip duplicates for the second and third numbers
                while left < right and nums[left] == nums[left + 1]:
                    left += 1
                while left < right and nums[right] == nums[right - 1]:
                    right -= 1

                left += 1
                right -= 1

    return result
```

## Time Complexity Analysis
> Time complexity  : O(n^2)
>
> Space complexity : O(n) — sorting (Python's Timsort); output not counted

## Related Problems
- [1. Two Sum](./1_two_sum.md) — 🟢 Easy · the pair-sum subproblem 3Sum reduces to
- [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted) — 🟡 Medium · the exact two-pointer inner loop
- [16. 3Sum Closest](https://leetcode.com/problems/3sum-closest) — 🟡 Medium · same sort + two pointers, tracking the closest sum
- [18. 4Sum](https://leetcode.com/problems/4sum) — 🟡 Medium · one more fixed index on top of 3Sum
