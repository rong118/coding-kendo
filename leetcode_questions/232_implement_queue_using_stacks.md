# 232. Implement Queue using Stacks

## Question link
(https://leetcode.com/problems/implement-queue-using-stacks/)

## Question Description
Implement a first-in-first-out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (`push`, `peek`, `pop`, and `empty`).

Implement the `MyQueue` class:

* `void push(int x)` Pushes element x to the back of the queue.
* `int pop()` Removes the element from the front of the queue and returns it.
* `int peek()` Returns the element at the front of the queue.
* `boolean empty()` Returns `true` if the queue is empty, `false` otherwise.

**Notes:**

* You must use **only** standard operations of a stack, which means only `push to top`, `peek/pop from top`, `size`, and `is empty` operations are valid.
* Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations.

Example 1:

> Input
> ["MyQueue", "push", "push", "peek", "pop", "empty"]
> [[], [1], [2], [], [], []]
> Output
> [null, null, null, 1, 1, false]
>
> Explanation
> MyQueue myQueue = new MyQueue();
> myQueue.push(1); // queue is: [1]
> myQueue.push(2); // queue is: [1, 2] (leftmost is front)
> myQueue.peek();  // return 1
> myQueue.pop();   // return 1, queue is [2]
> myQueue.empty(); // return false

Constraints:

* 1 <= x <= 9
* At most 100 calls will be made to `push`, `pop`, `peek`, and `empty`.
* All the calls to `pop` and `peek` are valid.

## Tags
- queue
- stack

## Code Implementation
```python
class MyQueue:
    def __init__(self):
        self.input = []   # push stack
        self.output = []  # pop/peek stack

    def push(self, x: int) -> None:
        self.input.append(x)

    def pop(self) -> int:
        self._transfer()
        return self.output.pop()

    def peek(self) -> int:
        self._transfer()
        return self.output[-1]

    def empty(self) -> bool:
        return not self.input and not self.output

    # Dump input stack into output stack when output is empty.
    # This reverses the order once, yielding FIFO from the output stack.
    def _transfer(self) -> None:
        if not self.output:
            while self.input:
                self.output.append(self.input.pop())
```

## Time Complexity Analysis
> Time complexity  : O(1) amortized — each element is pushed twice and popped twice across both stacks
>
> Space complexity : O(n) — elements stored across the two stacks
