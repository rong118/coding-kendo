# 1. Two Sum

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/two-sum/)

## Question Description
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

Example 1:
> Input: nums = [2,7,11,15], target = 9
>
> Output: [0,1]
>
> Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:
> Input: nums = [3,2,4], target = 6
>
> Output: [1,2]

Example 3:
> Input: nums = [3,3], target = 6
>
> Output: [0,1]

Constraints:
* 2 <= nums.length <= 10^4
* -10^9 <= nums[i] <= 10^9
* -10^9 <= target <= 10^9
* Only one valid answer exists.

## Tags
- array
- sort
- hashMap

## Approach
**Key idea:** For each number, the only partner that works is `target - num`; a hash map of values already seen answers "have I seen the complement?" in O(1).

1. Create an empty map from value to index.
2. Walk the array; for each `num` at index `i`, compute `complement = target - num`.
3. If `complement` is already in the map, return `[map[complement], i]`.
4. Otherwise store `num -> i` and continue (storing after the check prevents using the same element twice).

## Code Implementation
```python
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        # Dictionary to store number and its index
        num_to_index = {}
        
        for i, num in enumerate(nums):
            # Calculate the complement
            complement = target - num
            
            # Check if the complement exists in the dictionary
            if complement in num_to_index:
                return [num_to_index[complement], i]
            
            # Store the number with its index in the dictionary
            num_to_index[num] = i
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(n)

## Related Problems
- [15. 3Sum](./15_three_sum.md) — 🟡 Medium · extends the pair-sum idea to triplets
- [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted) — 🟡 Medium · same problem on sorted input, solved with two pointers
- [217. Contains Duplicate](./217_contain_duplicate.md) — 🟢 Easy · hash set lookup of previously seen values
- [49. Group Anagrams](./49_group_anagrams.md) — 🟡 Medium · hash map keyed by a derived value
