# Stack

A stack is a LIFO (Last-In-First-Out) data structure. Elements are pushed onto and popped from the top.

## Complexity

| Operation | Time |
|---|---|
| Push / Pop | O(1) |
| Peek (top) | O(1) |

## Python Usage

```python
stack = []
stack.append(10); stack.append(20)   # push
stack.pop()                           # pop — 20
stack[-1]                             # peek
```

## Related LeetCode Questions

- [155. Min Stack](../../leetcode_questions/155_min_stack.md)
- [232. Implement Stack Using Queues](../../leetcode_questions/232_implement_stack_using_queues.md)
- [716. Max Stack](../../leetcode_questions/716_max_stack.md)
- [895. Maximum Frequency Stack](../../leetcode_questions/895_maximum_frequency_stack.md)
- [1381. Design a Stack With Increment Operation](../../leetcode_questions/1381_design_a_stack_with_increment_operation.md)
