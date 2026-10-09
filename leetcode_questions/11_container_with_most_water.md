# 11. Container With Most Water

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/container-with-most-water)

## Question Description
You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

Example 1:

> Input: height = [1,8,6,2,5,4,8,3,7]
>
> Output: 49
>
> Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue 
>
> section) the container can contain is 49.

Example 2:

> Input: height = [1,1]
> Output: 1

Constraints:

* n == height.length
* 2 <= n <= 10^5
* 0 <= height[i] <= 10^4

## Tags
- array
- two pointers

## Approach
**Key idea:** The area is capped by the shorter line, so moving the taller pointer can never help — always move the shorter one inward.

1. Start with `l = 0` and `r = n - 1` (the widest container).
2. Compute `(r - l) * min(height[l], height[r])` and update the best answer.
3. Move the pointer at the shorter line inward; every other container using that line is narrower and no taller, so it can be discarded.
4. Stop when the pointers meet.

## Code Implementation
```python
class Solution:
    def maxArea(self, height: list[int]) -> int:
        l, r = 0, len(height) - 1
        best = 0
        while l < r:
            best = max(best, (r - l) * min(height[l], height[r]))
            if height[l] < height[r]:
                l += 1
            else:
                r -= 1
        return best
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1)

## Related Problems
- [42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water) — 🔴 Hard · two pointers moving the lower side inward
- [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted) — 🟡 Medium · two pointers from both ends
- [125. Valid Palindrome](./125_valid_palindrome.md) — 🟢 Easy · two pointers from both ends
