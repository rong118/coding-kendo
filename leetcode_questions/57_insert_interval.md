# 57. Insert Interval

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/insert-interval/)

## Question Description
You are given an array of non-overlapping intervals intervals where intervals[i] = [starti, endi] represent the start and the end of the ith interval and intervals is sorted in ascending order by starti. You are also given an interval newInterval = [start, end] that represents the start and end of another interval.

Insert newInterval into intervals such that intervals is still sorted in ascending order by starti and intervals still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return intervals after the insertion.

Example 1:

> Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
>
> Output: [[1,5],[6,9]]

Example 2:

> Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
>
> Output: [[1,2],[3,10],[12,16]]
>
> Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
 

Constraints:

- 0 <= intervals.length <= 104
- intervals[i].length == 2
- 0 <= starti <= endi <= 105
- intervals is sorted by starti in ascending order.
- newInterval.length == 2
- 0 <= start <= end <= 105

## Tags
- Array
- Sort

## Approach
**Key idea:** Adding the new interval and sorting by start turns the problem into a standard interval merge: once sorted, any overlapping intervals are adjacent.

1. Append `newInterval` to `intervals` and sort by start.
2. Keep a running interval `cur`, starting with the first one.
3. For each next interval: if it starts after `cur` ends, push `cur` to the answer and start a new `cur`.
4. Otherwise it overlaps, so extend `cur`'s end to the larger of the two ends.
5. Push the final `cur` after the loop.

## Code Implementation
```python
class Solution:
    def insert(self, intervals: list[list[int]], newInterval: list[int]) -> list[list[int]]:
        intervals = sorted(intervals + [newInterval])
        ans = []
        cur = intervals[0][:]
        for start, end in intervals[1:]:
            if start > cur[1]:
                ans.append(cur)
                cur = [start, end]
            else:
                cur[1] = max(cur[1], end)
        ans.append(cur)
        return ans
```

## Time Complexity Analysis
> Time complexity  : O(n log n) — dominated by the sort
>
> Space complexity : O(n) — sorted copy and output list

## Related Problems
- [56. Merge Intervals](./56_merge_intervals.md) — 🟡 Medium · the same sort-and-merge sweep
- [729. My Calendar I](./729_my_calendar_i.md) — 🟡 Medium · detecting overlap when inserting an interval
- [435. Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals) — 🟡 Medium · interval overlap after sorting
