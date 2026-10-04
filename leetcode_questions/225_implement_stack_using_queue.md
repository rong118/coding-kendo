# 225. Implement Stack using Queues

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/implement-stack-using-queues/)

## Question Description
Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (`push`, `top`, `pop`, and `empty`).

Implement the `MyStack` class:

* `void push(int x)` Pushes element x to the top of the stack.
* `int pop()` Removes the element on the top of the stack and returns it.
* `int top()` Returns the element on the top of the stack.
* `boolean empty()` Returns `true` if the stack is empty, `false` otherwise.

**Notes:**

* You must use **only** standard operations of a queue, which means only `push to back`, `peek/pop from front`, `size`, and `is empty` operations are valid.
* Depending on your language, the queue may not be supported natively. You may simulate a queue using a list or deque (double-ended queue) as long as you use only a queue's standard operations.

Example 1:

> Input
> ["MyStack", "push", "push", "top", "pop", "empty"]
> [[], [1], [2], [], [], []]
> Output
> [null, null, null, 2, 2, false]
>
> Explanation
> MyStack myStack = new MyStack();
> myStack.push(1);
> myStack.push(2);
> myStack.top();   // return 2
> myStack.pop();   // return 2
> myStack.empty(); // return False

Constraints:

* 1 <= x <= 9
* At most 100 calls will be made to `push`, `pop`, `top`, and `empty`.
* All the calls to `pop` and `top` are valid.

## Tags
- stack
- queue

## Approach
**Key idea:** Keep the queue in stack order — newest element at the front — by rotating all older elements behind each newly pushed one.

1. `push(x)`: append `x` to the back of the queue.
2. Then pop from the front and re-append `len(q) - 1` times, so `x` moves to the front.
3. `pop()` / `top()`: the front of the queue is the top of the stack.
4. `empty()`: the stack is empty when the queue is empty.

## Code Implementation
```python
from collections import deque

class MyStack:
    def __init__(self):
        self.q = deque()

    def push(self, x: int) -> None:
        # Push to back, then rotate all previous elements behind it
        self.q.append(x)
        for _ in range(len(self.q) - 1):
            self.q.append(self.q.popleft())

    def pop(self) -> int:
        return self.q.popleft()

    def top(self) -> int:
        return self.q[0]

    def empty(self) -> bool:
        return not self.q
```

## Time Complexity Analysis
> Time complexity  : O(n) for push (rotate n-1 elements); O(1) for pop, top, empty
>
> Space complexity : O(n) — elements stored in the queue

## Related Problems
- [232. Implement Queue using Stacks](./232_implement_queue_using_stacks.md) — 🟢 Easy · the mirror problem
- [155. Min Stack](./155_min_stack.md) — 🟡 Medium · stack design with an extra operation
- [716. Max Stack](./716_max_stack.md) — 🔴 Hard · stack design with an extra operation
