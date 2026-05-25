# 716. Max Stack

## Question link
(https://leetcode.com/problems/max-stack/)

## Question Description
Design a max stack that supports push, pop, top, peekMax and popMax.

push(x) -- Push element x onto stack.
pop() -- Remove the element on top of the stack and return it.
top() -- Get the element on the top.
peekMax() -- Retrieve the maximum element in the stack.
popMax() -- Retrieve the maximum element in the stack, and remove it. If you find more than one maximum elements, only remove the top-most one.

Example 1:

> MaxStack stack = new MaxStack();
> stack.push(5); 
> stack.push(1);
> stack.push(5);
> stack.top(); -> 5
> stack.popMax(); -> 5
> stack.top(); -> 1
> stack.peekMax(); -> 5
> stack.pop(); -> 1
> stack.top(); -> 5

Note:
- -1e<sup>7</sup> <= x <= 1e<sup>7</sup>
- Number of operations won't exceed 10000.
- The last four operations won't be called when stack is empty.

## Tags
- stack

## Code Implementation
```python
class MaxStack:
    def __init__(self):
        self.stack = []
        self.max_stack = []

    def push(self, x: int) -> None:
        self.stack.append(x)
        if not self.max_stack or x >= self.max_stack[-1]:
            self.max_stack.append(x)

    def pop(self) -> int:
        if self.stack[-1] == self.max_stack[-1]:
            self.max_stack.pop()
        return self.stack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def peekMax(self) -> int:
        return self.max_stack[-1]

    def popMax(self) -> int:
        mx = self.max_stack.pop()
        buf = []
        while self.stack[-1] != mx:
            buf.append(self.stack.pop())
        self.stack.pop()
        while buf:
            self.push(buf.pop())
        return mx
```

## Time Complexity Analysis
> Time complexity  : O(1) for push, pop, top, peekMax; O(n) for popMax
>
> Space complexity : O(n)
