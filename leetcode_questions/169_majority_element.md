# 169. Majority Element

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/majority-element/description/)

## Question Description
Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. 

You may assume that the majority element always exists in the array.

Example 1:

> Input: nums = [3,2,3]
>
> Output: 3

Example 2:

> Input: nums = [2,2,1,1,1,2,2]
>
> Output: 2

Constraints:

- n == nums.length
- 1 <= n <= 5 * 104
- -109 <= nums[i] <= 109

## Tags
- array

## Approach
**Key idea:** Boyer-Moore voting: pair each majority element with a different element and cancel both out. Since the majority appears more than n / 2 times, it is the one left at the end.

1. Keep a `candidate` and a `count`, starting at `count = 0`.
2. For each number, if `count` is 0, make this number the new candidate.
3. Add 1 to `count` if the number equals the candidate, otherwise subtract 1.
4. After the pass, `candidate` is the majority element (the problem guarantees one exists).

## Code Implementation
```python
class Solution:
    # Boyer-Moore Voting Algorithm
    def majorityElement(self, nums: list[int]) -> int:
        count = 0
        candidate = None

        for num in nums:
            if count == 0:
                candidate = num
            count += (1 if num == candidate else -1)

        return candidate
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1)

## Related Problems
- [229. Majority Element II](https://leetcode.com/problems/majority-element-ii) — 🟡 Medium · Boyer-Moore voting with two candidates
- [347. Top K Frequent Elements](./347_top_k_frequent_elements.md) — 🟡 Medium · finding the most frequent elements
- [217. Contains Duplicate](./217_contain_duplicate.md) — 🟢 Easy · counting occurrences in an array
