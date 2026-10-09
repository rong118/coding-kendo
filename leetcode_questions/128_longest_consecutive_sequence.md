# 128. Longest Consecutive Sequence

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/longest-consecutive-sequence/)

## Question Description
Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in **O(n)** time.

Example 1:

> Input: nums = [100,4,200,1,3,2]
>
> Output: 4
>
> Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.

Example 2:

> Input: nums = [0,3,7,2,5,8,4,6,0,1]
>
> Output: 9

Constraints:

* 0 <= nums.length <= 10^5
* -10^9 <= nums[i] <= 10^9

## Tags
- hashset

## Approach
**Key idea:** Put the numbers in a hash set and only start counting from a number whose predecessor (`num - 1`) is missing, so each sequence is walked only once.

1. Build a set of all numbers so lookups are O(1).
2. For each number, skip it if `num - 1` is in the set (it is not the start of a sequence).
3. Otherwise, count upward while `num + 1`, `num + 2`, ... are in the set.
4. Keep the longest streak seen and return it.

## Code Implementation
```python
class Solution:
    def longestConsecutive(self, nums: list[int]) -> int:
        num_set = set(nums)
        longest = 0

        for num in num_set:
            # Only start counting from the beginning of a sequence
            if num - 1 not in num_set:
                cur = num
                streak = 1
                while cur + 1 in num_set:
                    cur += 1
                    streak += 1
                longest = max(longest, streak)

        return longest
```

## Time Complexity Analysis
> Time complexity  : O(n) — each element is visited at most twice (once as a start, once within a streak)
>
> Space complexity : O(n) — the hash set

## Related Problems
- [549. Binary Tree Longest Consecutive Sequence II](./549_binary_tree_longest_consecutive_sequence_ii.md) — 🟡 Medium · longest consecutive run, but along a tree path
- [298. Binary Tree Longest Consecutive Sequence](https://leetcode.com/problems/binary-tree-longest-consecutive-sequence) — 🟡 Medium · consecutive run along parent-child paths
- [217. Contains Duplicate](./217_contain_duplicate.md) — 🟢 Easy · hash set membership checks
