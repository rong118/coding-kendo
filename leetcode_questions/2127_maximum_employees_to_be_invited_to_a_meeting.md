# 2127. Maximum Employees to Be Invited to a Meeting

**Difficulty:** 🔴 Hard

## Question link
(https://leetcode.com/problems/maximum-employees-to-be-invited-to-a-meeting/)

## Question Description
A company is organizing a meeting and has a list of n employees, waiting to be invited. They have arranged for a large circular table, capable of seating any number of employees.

The employees are numbered from 0 to n - 1. Each employee has a favorite person and they will attend the meeting only if they can sit next to their favorite person at the table. The favorite person of an employee is not themself.

Given a 0-indexed integer array favorite, where favorite[i] denotes the favorite person of the ith employee, return the maximum number of employees that can be invited to the meeting.

<br/>

Example 1:
> <img src="https://assets.leetcode.com/uploads/2021/12/14/ex1.png" width="200" />
>
> Input: favorite = [2,2,1,2]
>
> Output: 3
>
> Explanation:
>
> The above figure shows how the company can invite employees 0, 1, and 2, and seat them at the round table.
>
> All employees cannot be invited because employee 2 cannot sit beside employees 0, 1, and 3, simultaneously.
>
> Note that the company can also invite employees 1, 2, and 3, and give them their desired seats.
>
> The maximum number of employees that can be invited to the meeting is 3.

Example 2:
> Input: favorite = [1,2,0]
>
> Output: 3
>
> Explanation: 
>
> Each employee is the favorite person of at least one other employee, and the only way the company can invite them is if they invite every employee.
>
> The seating arrangement will be the same as that in the figure given in example 1:
>
> - Employee 0 will sit between employees 2 and 1.
>
> - Employee 1 will sit between employees 0 and 2.
>
> - Employee 2 will sit between employees 1 and 0.
>
> The maximum number of employees that can be invited to the meeting is 3.

Example 3:
> <img src="https://assets.leetcode.com/uploads/2021/12/14/ex2.png" width="200" />
>
> Input: favorite = [3,0,1,4,1]
>
> Output: 4
>
> Explanation:
>
> The above figure shows how the company will invite employees 0, 1, 3, and 4, and seat them at the round table.
>
> Employee 2 cannot be invited because the two spots next to their favorite employee 1 are taken.
>
> So the company leaves them out of the meeting.
>
> The maximum number of employees that can be invited to the meeting is 4.

Constraints:
- n == favorite.length
- 2 <= n <= 10<sup>power</sup> 
- 0 <= favorite[i] <= n - 1
- favorite[i] != i

## Tags
- graph
- topologic sort

## Approach
**Key idea:** `i -> favorite[i]` is a functional graph: each component is one cycle with chains feeding into it. A cycle of length ≥ 3 must be seated alone, while every mutual pair (cycle of length 2) can bring the longest chain into each side, and all such pair-groups fit at the table together.

1. Compute indegrees and run Kahn's topological sort to strip every node that is not on a cycle.
2. While stripping, record `depth[v]` = longest chain of people ending at `v` (including `v`).
3. Walk each remaining cycle once to get its length.
4. For a cycle of length 2 `(a, b)`, add `depth[a] + depth[b]` to a running total; for longer cycles keep the maximum length.
5. Return the larger of the longest cycle and the total over all mutual pairs.

## Code Implementation
```python
from collections import deque


class Solution:
    def maximumInvitations(self, favorite: list[int]) -> int:
        n = len(favorite)
        indegree = [0] * n
        for f in favorite:
            indegree[f] += 1

        # Peel off nodes that are not on a cycle (Kahn's), tracking the
        # longest chain of people that ends at each node.
        depth = [1] * n
        q = deque(i for i in range(n) if indegree[i] == 0)
        while q:
            u = q.popleft()
            v = favorite[u]
            depth[v] = max(depth[v], depth[u] + 1)
            indegree[v] -= 1
            if indegree[v] == 0:
                q.append(v)

        # Every remaining node (indegree > 0) lies on a cycle.
        longest_cycle = 0
        pairs_total = 0
        for i in range(n):
            if indegree[i] == 0:
                continue
            length, j = 0, i
            while indegree[j]:
                indegree[j] = 0  # mark visited
                length += 1
                j = favorite[j]
            if length == 2:
                # Mutual pair: both chains hanging off it can sit in a row,
                # and all such groups can share the table.
                pairs_total += depth[i] + depth[favorite[i]]
            else:
                longest_cycle = max(longest_cycle, length)

        return max(longest_cycle, pairs_total)
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(n) — indegree, depth, and queue arrays

## Related Problems
- [2360. Longest Cycle in a Graph](https://leetcode.com/problems/longest-cycle-in-a-graph) — 🔴 Hard · cycle lengths in a functional graph
- [802. Find Eventual Safe States](https://leetcode.com/problems/find-eventual-safe-states) — 🟡 Medium · Kahn's peeling to separate cycle nodes
- [207. Course Schedule](./207_course_schedule.md) — 🟡 Medium · topological sort for cycle detection
