# 217. Contains Duplicate

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/contains-duplicate/)

## Question Description
Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

Example 1:

> Input: nums = [1,2,3,1]
>
> Output: true

Example 2:

> Input: nums = [1,2,3,4]
>
> Output: false

Example 3:

> Input: nums = [1,1,1,3,3,4,3,2,4,2]
>
> Output: true

Constraints:
- 1 <= nums.length <= 10^5
- -10^9 <= nums[i] <= 10^9

## Tags
- array
- sort
- hashing

## Approach
**Key idea:** A hash set gives O(1) membership checks, so the first time a number is already in the set we have found a duplicate.

1. Start with an empty set `seen`.
2. For each number, if it is already in `seen`, return `True`.
3. Otherwise add it to `seen`.
4. If the loop finishes, every element was distinct — return `False`.

## Code Implementation
```python
class Solution:
    def containsDuplicate(self, nums: list[int]) -> bool:
        seen = set()
        for num in nums:
            if num in seen:
                return True
            seen.add(num)
        return False
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(n)

## Related Problems
- [1. Two Sum](./1_two_sum.md) — 🟢 Easy · hash lookup of previously seen values
- [242. Valid Anagram](./242_valid_anagram.md) — 🟢 Easy · hashing to compare element counts
- [287. Find the Duplicate Number](./287_find_the_duplicate_number.md) — 🟡 Medium · find the duplicate under O(1) space
- [219. Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii) — 🟢 Easy · duplicate within a distance k
