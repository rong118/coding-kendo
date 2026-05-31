# 981. Time Based Key-Value Store

## Question link
(https://leetcode.com/problems/time-based-key-value-store/)

## Question Description
Design a time-based key-value data structure that can store multiple values for the same key at different timestamps and retrieve the key's value at a certain timestamp.

Implement the `TimeMap` class:

* `TimeMap()` Initializes the object.
* `void set(String key, String value, int timestamp)` Stores the key `key` with value `value` at the given time `timestamp`.
* `String get(String key, int timestamp)` Returns a value such that `set` was called previously, with `timestamp_prev <= timestamp`. If there are multiple such values, return the value associated with the largest `timestamp_prev`. If there are no values, return `""`.

Example 1:

> Input
> ["TimeMap", "set", "get", "get", "set", "get", "get"]
> [[], ["foo", "bar", 1], ["foo", 1], ["foo", 3], ["foo", "bar2", 4], ["foo", 4], ["foo", 5]]
> Output
> [null, null, "bar", "bar", null, "bar2", "bar2"]
>
> Explanation
> TimeMap timeMap = new TimeMap();
> timeMap.set("foo", "bar", 1);  // store key "foo" and value "bar" at timestamp 1
> timeMap.get("foo", 1);         // return "bar"
> timeMap.get("foo", 3);         // return "bar" (no value at timestamp 3, closest earlier is 1)
> timeMap.set("foo", "bar2", 4); // store key "foo" and value "bar2" at timestamp 4
> timeMap.get("foo", 4);         // return "bar2"
> timeMap.get("foo", 5);         // return "bar2" (no value at timestamp 5, closest earlier is 4)

Constraints:

* 1 <= key.length, value.length <= 100
* key and value consist of lowercase English letters and digits.
* 1 <= timestamp <= 10^7
* All timestamps of `set` calls are strictly increasing.
* At most 2 * 10^5 calls will be made to `set` and `get`.

## Tags
- treemap

## Code Implementation
```python
from sortedcontainers import SortedDict

class TimeMap:
    def __init__(self):
        # key → SortedDict(timestamp → value)
        self.store: dict[str, SortedDict] = {}

    def set(self, key: str, value: str, timestamp: int) -> None:
        if key not in self.store:
            self.store[key] = SortedDict()
        self.store[key][timestamp] = value

    def get(self, key: str, timestamp: int) -> str:
        if key not in self.store:
            return ""

        # SortedDict.bisect_right returns the index after the last key ≤ timestamp,
        # so we look one position back for the floor.
        sd = self.store[key]
        idx = sd.bisect_right(timestamp) - 1
        if idx < 0:
            return ""
        return sd.peekitem(idx)[1]
```

## Time Complexity Analysis
> Time complexity  : O(log n) for both set and get — SortedDict insertion and bisect are O(log n)
>
> Space complexity : O(n) — stores all key/timestamp/value tuples
