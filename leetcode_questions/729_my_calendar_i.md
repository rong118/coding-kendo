# 729. My Calendar I

## Question link
(https://leetcode.com/problems/my-calendar-i/)

## Question Description
You are implementing a program to use as your calendar. We can add a new event if adding the event will not cause a **double booking**.

A **double booking** happens when two events have some non-empty intersection (i.e., some moment is common to both events).

The event can be represented as a pair of integers `start` and `end` that represents a booking on the half-open interval `[start, end)`, the range of real numbers `x` such that `start <= x < end`.

Implement the `MyCalendar` class:

* `MyCalendar()` Initializes the calendar object.
* `boolean book(int start, int end)` Returns `true` if the event can be added to the calendar successfully without causing a double booking. Otherwise, return `false` and do not add the event to the calendar.

Example 1:

> Input
> ["MyCalendar", "book", "book", "book"]
> [[], [10, 20], [15, 25], [20, 30]]
> Output
> [null, true, false, true]
>
> Explanation
> MyCalendar myCalendar = new MyCalendar();
> myCalendar.book(10, 20); // return True
> myCalendar.book(15, 25); // return False (overlaps with [10, 20))
> myCalendar.book(20, 30); // return True (adjacent, no overlap)

Constraints:

* 0 <= start < end <= 10^9
* At most 1000 calls will be made to `book`.

## Tags
- treemap

## Code Implementation
```python
from sortedcontainers import SortedDict

class MyCalendar:
    def __init__(self):
        # SortedDict mapping start → end for all booked intervals
        self.events = SortedDict()

    def book(self, start: int, end: int) -> bool:
        # Find the interval that would come before and after [start, end)
        idx = self.events.bisect_left(start)

        # Check previous interval — does it overlap?
        if idx > 0:
            prev_start, prev_end = self.events.peekitem(idx - 1)
            if prev_end > start:
                return False

        # Check next interval — does it overlap?
        if idx < len(self.events):
            next_start, next_end = self.events.peekitem(idx)
            if next_start < end:
                return False

        # No overlap — book it
        self.events[start] = end
        return True
```

## Time Complexity Analysis
> Time complexity  : O(log n) per book — bisect_left and insertion on SortedDict are O(log n)
>
> Space complexity : O(n) — stores all booked intervals
