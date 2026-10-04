# 39. Combination Sum

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/combination-sum/description/)

## Question Description
Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order.

The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the 
frequency
 of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to target is less than 150 combinations for the given input.

Example 1:

> Input: candidates = [2,3,6,7], target = 7
> 
> Output: [[2,2,3],[7]]
> 
> Explanation:
> 
> 2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
>
> 7 is a candidate, and 7 = 7.
>
> These are the only two combinations.

Example 2:

> Input: candidates = [2,3,5], target = 8
>
> Output: [[2,2,2,2],[2,3,3],[3,5]]

Example 3:

> Input: candidates = [2], target = 1
>
> Output: []
 

Constraints:
* 1 <= candidates.length <= 30
* 2 <= candidates[i] <= 40
* All elements of candidates are distinct.
* 1 <= target <= 40

## Tags
- array
- dfs
- backtracking

## Approach
**Key idea:** Build combinations in non-decreasing index order — each recursive call may only pick candidates from `start` onward — so every multiset is generated exactly once; sorting lets the loop stop as soon as a candidate exceeds the remaining target.

1. Sort `candidates`.
2. Backtrack with a current `path`, a `start` index, and the `remain`ing target.
3. If `remain == 0`, save a copy of `path`.
4. Otherwise try each candidate from `start` on; stop the loop once a candidate is larger than `remain`.
5. Recurse with the same index `i` (the number can be reused), then pop it to undo the choice.

## Code Implementation
```python
class Solution:
    def combinationSum(self, candidates: list[int], target: int) -> list[list[int]]:
        candidates.sort()
        ans: list[list[int]] = []
        path: list[int] = []

        def backtrack(start: int, remain: int) -> None:
            if remain == 0:
                ans.append(path[:])
                return
            for i in range(start, len(candidates)):
                if candidates[i] > remain:
                    break  # sorted, so every later candidate is too big as well
                path.append(candidates[i])
                backtrack(i, remain - candidates[i])  # i, not i + 1: reuse allowed
                path.pop()

        backtrack(0, target)
        return ans
```

## Time Complexity Analysis
> Time complexity  : O(n^(t/m + 1)) — n candidates, t = target, m = smallest candidate (max depth is t/m)
>
> Space complexity : O(t/m) — recursion depth and current path; output not counted

## Related Problems
- [40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii) — 🟡 Medium · each number used at most once, with duplicates in input
- [216. Combination Sum III](https://leetcode.com/problems/combination-sum-iii) — 🟡 Medium · same backtracking with a fixed combination size
- [377. Combination Sum IV](https://leetcode.com/problems/combination-sum-iv) — 🟡 Medium · counts ordered combinations with DP instead
- [46. Permutations](https://leetcode.com/problems/permutations) — 🟡 Medium · classic backtracking template
