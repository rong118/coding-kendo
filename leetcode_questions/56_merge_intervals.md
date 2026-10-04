# 56. Merge Intervals

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/merge-intervals/)

## Question Description
Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

Example 1:

> Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
>
> Output: [[1,6],[8,10],[15,18]]
>
> Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

Example 2:

> Input: intervals = [[1,4],[4,5]]
>
> Output: [[1,5]]
>
> Explanation: Intervals [1,4] and [4,5] are considered overlapping.
 
Constraints:

- 1 <= intervals.length <= 10^4
- intervals[i].length == 2
- 0 <= starti <= endi <= 10^4

## Tags
- Array
- Sort

## Approach
**Key idea:** After sorting by start, any interval that overlaps the current merged block must come right after it, so a single left-to-right pass is enough.

1. Sort the intervals by start (then end).
2. Start the result with a copy of the first interval.
3. For each next interval, if its start is greater than the end of the last merged interval, there is a gap, so append it as a new block.
4. Otherwise it overlaps (touching counts), so extend the last block's end to `max(end, current_end)`.
5. Return the merged list.

## Code Implementation
```python
class Solution:
    def merge(self, intervals: list[list[int]]) -> list[list[int]]:
        intervals.sort()
        merged = [intervals[0][:]]
        for start, end in intervals[1:]:
            if start > merged[-1][1]:
                merged.append([start, end])
            else:
                merged[-1][1] = max(merged[-1][1], end)
        return merged
```

## Time Complexity Analysis
> Time complexity  : O(n log n) — dominated by sorting
>
> Space complexity : O(n) — output list (plus sort space)

## Related Problems
- [57. Insert Interval](./57_insert_interval.md) — 🟡 Medium · merge one new interval into sorted intervals
- [729. My Calendar I](./729_my_calendar_i.md) — 🟡 Medium · interval overlap checks
- [252. Meeting Rooms](https://leetcode.com/problems/meeting-rooms) — 🟢 Easy · sort by start and check adjacent overlaps
