# 189. Rotate Array

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/rotate-array/)

## Question Description
Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.

Example 1:

> Input: nums = [1,2,3,4,5,6,7], k = 3
>
> Output: [5,6,7,1,2,3,4]
>
> Explanation:
>
> rotate 1 steps to the right: [7,1,2,3,4,5,6]
>
> rotate 2 steps to the right: [6,7,1,2,3,4,5]
>
> rotate 3 steps to the right: [5,6,7,1,2,3,4]

Example 2:

> Input: nums = [-1,-100,3,99], k = 2
>
> Output: [3,99,-1,-100]
>
> Explanation:
>
> rotate 1 steps to the right: [99,-1,-100,3]
>
> rotate 2 steps to the right: [3,99,-1,-100]

Constraints:

- 1 <= nums.length <= 10⁵
- -2³¹ <= nums[i] <= 2³¹ - 1
- 0 <= k <= 10⁵

## Tags
- array
- in-place

## Approach
**Key idea:** Rotating right by `k` moves the last `k` elements to the front; reversing the whole array and then reversing each of the two parts restores their internal order in place.

1. Reduce `k` modulo `n`, since rotating by `n` is a no-op.
2. Reverse the entire array.
3. Reverse the first `k` elements.
4. Reverse the remaining `n - k` elements.

## Code Implementation
```python
def rotate(nums, k):
    k %= len(nums)

    def reverse(l, r):
        while l < r:
            nums[l], nums[r] = nums[r], nums[l]
            l += 1
            r -= 1

    reverse(0, len(nums) - 1)   # reverse whole array
    reverse(0, k - 1)           # reverse first k elements
    reverse(k, len(nums) - 1)   # reverse remaining elements
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1)

## Related Problems
- [61. Rotate List](https://leetcode.com/problems/rotate-list) — 🟡 Medium · same rotation on a linked list
- [151. Reverse Words in a String](./151_reverse_words_in_a_string.md) — 🟡 Medium · reverse-the-whole-then-the-parts trick
- [344. Reverse String](./344_reverse_string.md) — 🟢 Easy · the two-pointer reverse helper
- [48. Rotate Image](./48_rotate_image.md) — 🟡 Medium · in-place rotation via reversals/transposes
