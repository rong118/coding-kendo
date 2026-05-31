# Stack & Queue

Stack (LIFO) and Queue (FIFO) are fundamental linear data structures that differ only in removal order. Together they underpin traversal, backtracking, buffering, and scheduling.

## Stack — Last-In-First-Out

Elements are pushed onto and popped from the **top**. The last element added is the first removed.

### Complexity

| Operation | Time |
|---|---|
| Push / Pop | O(1) |
| Peek (top) | O(1) |

### Python Usage

```python
stack = []
stack.append(10); stack.append(20)   # push
stack.pop()                           # pop — 20
stack[-1]                             # peek
```

## Queue — First-In-First-Out

Elements are added at the **rear** and removed from the **front**. The first element added is the first removed.

### Complexity

| Operation | Time |
|---|---|
| Enqueue / Dequeue | O(1) |
| Peek (front) | O(1) |

### Python Usage

```python
from collections import deque

q = deque()
q.append(10); q.append(20)   # enqueue
q.popleft()                    # dequeue — 10
q[0]                           # peek front
```

## Deque — Double-Ended Queue

A deque supports insertion and deletion from **both ends**.

```python
from collections import deque

dq = deque([1, 2, 3])
dq.append(4); dq.appendleft(0)  # add right/left
dq.pop(); dq.popleft()          # remove right/left
dq.rotate(2)                    # rotate right by 2
```

## Related LeetCode Questions

### Stack

| # | Problem | Technique |
|---|---------|-----------|
| 155 | [Min Stack](../../leetcode_questions/155_min_stack.md) | Auxiliary min-stack tracking |
| 225 | [Implement Stack using Queues](../../leetcode_questions/225_implement_stack_using_queue.md) | Single-queue rotation |
| 1381 | [Design a Stack With Increment Operation](../../leetcode_questions/1381_design_a_stack_with_increment_operation.md) | Lazy increment array |

### Queue

| # | Problem | Technique |
|---|---------|-----------|
| 232 | [Implement Queue using Stacks](../../leetcode_questions/232_implement_queue_using_stacks.md) | Two-stack transfer |
| 622 | [Design Circular Queue](../../leetcode_questions/622_design_circular_queue.md) | Ring buffer with modulo arithmetic |
| 641 | [Design Circular Deque](../../leetcode_questions/641_design_circular_deque.md) | Circular array with front/rear pointers |
