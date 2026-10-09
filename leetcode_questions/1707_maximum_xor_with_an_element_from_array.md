# 1707. Maximum XOR With an Element From Array

**Difficulty:** 🔴 Hard

## Question link
(https://leetcode.com/problems/maximum-xor-with-an-element-from-array/)

## Question Description
You are given an array nums consisting of non-negative integers. You are also given a queries array, where queries[i] = [xi, mi].

The answer to the ith query is the maximum bitwise XOR value of xi and any element of nums that does not exceed mi. In other words, the answer is max(nums[j] XOR xi) for all j such that nums[j] <= mi. If all elements in nums are larger than mi, then the answer is -1.

Return an integer array answer where answer.length == queries.length and answer[i] is the answer to the ith query.

> Example 1:
>
> Input: nums = [0,1,2,3,4], queries = [[3,1],[1,3],[5,6]]
>
> Output: [3,3,7]
>
> Explanation:
> - 0 and 1 are the only two integers not greater than 1. 0 XOR 3 = 3 and 1 XOR 3 = 2. The larger of the two is 3.
> - 1 XOR 2 = 3.
> - 5 XOR 2 = 7.

> Example 2:
>
> Input: nums = [5,2,4,6,6,3], queries = [[12,4],[8,1],[6,3]]
>
> Output: [15,-1,5]

Constraints:
- 1 <= nums.length, queries.length <= 10<sup>5</sup>
- queries[i].length == 2
- 0 <= nums[j], xi, mi <= 10<sup>9</sup>

## Tags
- trie
- bitwise

## Approach
**Key idea:** Answer queries offline in increasing order of `m`, inserting only the numbers `<= m` into a binary trie; then the maximum XOR is found greedily by taking the opposite bit at each level whenever possible.

1. Sort `nums`, and sort query indices by their limit `m`.
2. For each query, insert into the trie every remaining number `<= m` (bits from high to low).
3. If the trie is still empty, the answer is `-1`.
4. Otherwise walk the trie from the highest bit: prefer the child with the opposite bit of `x` (that bit becomes 1 in the XOR), else take the same bit.
5. Store the XOR at the query's original index.

## Code Implementation
```python
class Solution:
    def maximizeXor(self, nums: list[int], queries: list[list[int]]) -> list[int]:
        BITS = 30  # 10^9 < 2^30
        nums.sort()
        order = sorted(range(len(queries)), key=lambda i: queries[i][1])

        root = {}
        ans = [-1] * len(queries)
        j = 0
        for qi in order:
            x, m = queries[qi]
            # Insert every number <= m into the trie
            while j < len(nums) and nums[j] <= m:
                node = root
                for b in range(BITS - 1, -1, -1):
                    node = node.setdefault((nums[j] >> b) & 1, {})
                j += 1

            if not root:
                continue  # no number <= m, answer stays -1

            # Greedily pick the opposite bit at each level
            node, xor = root, 0
            for b in range(BITS - 1, -1, -1):
                bit = (x >> b) & 1
                if 1 - bit in node:
                    xor |= 1 << b
                    node = node[1 - bit]
                else:
                    node = node[bit]
            ans[qi] = xor
        return ans
```

## Time Complexity Analysis
> Time complexity  : O(n log n + q log q + (n + q) · L) — sorting plus L = 30 trie steps per insert and query
>
> Space complexity : O(n · L + q) — trie nodes and the answer array

## Related Problems
- [421. Maximum XOR of Two Numbers in an Array](./421_maximum_xor_of_numbers_in_an_array.md) — 🟡 Medium · same greedy binary-trie XOR
- [208. Implement Trie (Prefix Tree)](./208_implement_trie.md) — 🟡 Medium · trie fundamentals
- [1938. Maximum Genetic Difference Query](https://leetcode.com/problems/maximum-genetic-difference-query) — 🔴 Hard · offline queries with a binary XOR trie
