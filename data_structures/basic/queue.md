# Queue

A queue is a FIFO (First-In-First-Out) data structure. Elements are added at the rear and removed from the front.

## Complexity

| Operation | Time |
|---|---|
| Enqueue / Dequeue | O(1) |
| Peek (front) | O(1) |

## Python Usage

```python
from collections import deque

q = deque()
q.append(10); q.append(20)   # enqueue
q.popleft()                    # dequeue — 10
q[0]                           # peek front
```

## Deque (Double-Ended Queue)

A deque supports insertion and deletion from both ends.

```python
from collections import deque

dq = deque([1, 2, 3])
dq.append(4); dq.appendleft(0)  # add right/left
dq.pop(); dq.popleft()          # remove right/left
dq.rotate(2)                    # rotate right by 2
```

## Related LeetCode Questions

- [225. Implement Stack using Queues](../../leetcode_questions/225_implement_stack_using_queue.md)
- [622. Design Circular Queue](../../leetcode_questions/622_design_circular_queue.md)
- [641. Design Circular Deque](../../leetcode_questions/641_design_circular_deque.md)
