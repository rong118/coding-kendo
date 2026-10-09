# 421. Maximum XOR of Two Numbers in an Array

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/)

## Question Description
Given an integer array nums, return the maximum result of nums[i] XOR nums[j], where 0 <= i <= j < n.

> Example 1:
>
> Input: nums = [3,10,5,25,2,8]
>
> Output: 28
>
> Explanation: The maximum result is 5 XOR 25 = 28.

> Example 2:
>
> Input: nums = [0]
>
> Output: 0

> Example 3:
>
> Input: nums = [2,4]
>
> Output: 6

> Example 4:
>
> Input: nums = [8,10,2]
>
> Output: 10

> Example 5:
>
> Input: nums = [14,70,53,83,49,91,36,80,92,51,66,70]
>
> Output: 127

Constraints:
- 1 <= nums.length <= 2 * 10<sup>5</sup>
- 0 <= nums[i] <= 2<sup>31</sup> - 1

## Tags
- trie
- bitwise
- bitwise trie 存入数字后，再次遍历从最高位找相反的bit，则可以形成最大的XOR,因为XOR只有不同才能留下

## Approach
**Key idea:** XOR is maximized greedily from the most significant bit down: for each number, try to follow the opposite bit at every level of a binary trie built from all numbers, since a 1 in a higher bit beats any combination of lower bits.

1. Insert every number into a binary trie, bit 31 down to bit 0 (each node has a `0` and a `1` child).
2. For each number, walk the trie from the top bit; at each bit prefer the child with the opposite bit.
3. If the opposite child exists, set that bit in the running XOR and follow it; otherwise follow the same-bit child.
4. The answer is the largest XOR found across all numbers.

## Code Implementation
```python
class TrieNode:
    def __init__(self):
        self.children: list["TrieNode | None"] = [None, None]


class Solution:
    def findMaximumXOR(self, nums: list[int]) -> int:
        root = TrieNode()
        for num in nums:
            node = root
            for i in range(31, -1, -1):
                bit = (num >> i) & 1
                if node.children[bit] is None:
                    node.children[bit] = TrieNode()
                node = node.children[bit]

        best = 0
        for num in nums:
            node, cur = root, 0
            for i in range(31, -1, -1):
                bit = (num >> i) & 1
                if node.children[1 - bit] is not None:
                    cur |= 1 << i
                    node = node.children[1 - bit]
                else:
                    node = node.children[bit]
            best = max(best, cur)
        return best
```

## Time Complexity Analysis
> Time complexity  : O(32 · n) = O(n) — each number is inserted and queried in 32 steps
>
> Space complexity : O(32 · n) = O(n) — up to 32 trie nodes per number

## Related Problems
- [1707. Maximum XOR With an Element From Array](./1707_maximum_xor_with_an_element_from_array.md) — 🔴 Hard · same bitwise trie with offline queries
- [208. Implement Trie](./208_implement_trie.md) — 🟡 Medium · the underlying trie data structure
- [1803. Count Pairs With XOR in a Range](https://leetcode.com/problems/count-pairs-with-xor-in-a-range) — 🔴 Hard · bitwise trie with subtree counts
