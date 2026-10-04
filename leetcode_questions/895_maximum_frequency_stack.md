# 895. Maximum Frequency Stack

**Difficulty:** 🔴 Hard

## Question link
(https://leetcode.com/problems/maximum-frequency-stack/)

## Question Description
Design a stack-like data structure to push elements to the stack and pop the most frequent element from the stack.

Implement the FreqStack class:
- FreqStack() constructs an empty frequency stack.
- void push(int val) pushes an integer val onto the top of the stack.
- int pop() removes and returns the most frequent element in the stack.
- If there is a tie for the most frequent element, the element closest to the stack's top is removed and returned.

Example 1:

> Input
> ["FreqStack", "push", "push", "push", "push", "push", "push", "pop", "pop", "pop", "pop"]
> [[], [5], [7], [5], [7], [4], [5], [], [], [], []]
> Output
> [null, null, null, null, null, null, null, 5, 7, 5, 4]
>
> Explanation
> FreqStack freqStack = new FreqStack();
> freqStack.push(5); // The stack is [5]
> freqStack.push(7); // The stack is [5,7]
> freqStack.push(5); // The stack is [5,7,5]
> freqStack.push(7); // The stack is [5,7,5,7]
> freqStack.push(4); // The stack is [5,7,5,7,4]
> freqStack.push(5); // The stack is [5,7,5,7,4,5]
> freqStack.pop();   // return 5, as 5 is the most frequent. The stack becomes [5,7,5,7,4].
> freqStack.pop();   // return 7, as 5 and 7 is the most frequent, but 7 is closest to the top. The stack becomes [5,7,5,4].
> freqStack.pop();   // return 5, as 5 is the most frequent. The stack becomes [5,7,4].
> freqStack.pop();   // return 4, as 4, 5 and 7 is the most frequent, but 4 is closest to the top. The stack becomes [5,7].

Constraints:
- 0 <= val <= 10<sup>9</sup>
- At most 2 * 10<sup>4</sup> calls will be made to push and pop.
- It is guaranteed that there will be at least one element in the stack before calling pop.

## Tags
- stack

## Approach
**Key idea:** Keep a separate stack for each frequency level. When a value reaches frequency `f`, push it onto stack `f`. The top of the highest-frequency stack is then the most frequent value, and the most recent one if there is a tie.

1. `freq[val]` counts each value; `group[f]` is a stack of values that reached frequency `f`; `max_freq` tracks the highest level.
2. `push`: increment `freq[val]` to `f`, update `max_freq`, and push `val` onto `group[f]`.
3. `pop`: pop from `group[max_freq]` and decrement that value's frequency.
4. If `group[max_freq]` is now empty, decrement `max_freq`.
5. Copies of the value at lower levels stay in place, so later pops still find it there.

## Code Implementation
```python
class FreqStack:
    def __init__(self):
        self.freq = {}
        self.group = {}
        self.max_freq = 0

    def push(self, val: int) -> None:
        self.freq[val] = self.freq.get(val, 0) + 1
        f = self.freq[val]
        self.max_freq = max(self.max_freq, f)
        if f not in self.group:
            self.group[f] = []
        self.group[f].append(val)

    def pop(self) -> int:
        val = self.group[self.max_freq].pop()
        self.freq[val] -= 1
        if not self.group[self.max_freq]:
            self.max_freq -= 1
        return val
```

## Time Complexity Analysis
> Time complexity  : O(1) for both push and pop
>
> Space complexity : O(n)

## Related Problems
- [716. Max Stack](./716_max_stack.md) — 🔴 Hard · stack that pops by a priority
- [155. Min Stack](./155_min_stack.md) — 🟡 Medium · stack with O(1) extra queries
- [460. LFU Cache](https://leetcode.com/problems/lfu-cache) — 🔴 Hard · buckets keyed by frequency
