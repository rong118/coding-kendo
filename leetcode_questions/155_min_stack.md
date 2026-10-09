# 155. Min Stack

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/min-stack/)

## Question Description
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the MinStack class:

MinStack() initializes the stack object.
void push(int val) pushes the element val onto the stack.
void pop() removes the element on the top of the stack.
int top() gets the top element of the stack.
int getMin() retrieves the minimum element in the stack.

Example 1:
> Input
> ["MinStack","push","push","push","getMin","pop","top","getMin"]
> [[],[-2],[0],[-3],[],[],[],[]]
>
> Output
> [null,null,null,null,-3,null,0,-2]
>
> Explanation
> MinStack minStack = new MinStack();
> minStack.push(-2);
> minStack.push(0);
> minStack.push(-3);
> minStack.getMin(); // return -3
> minStack.pop();
> minStack.top();    // return 0
> minStack.getMin(); // return -2

Constraints:
- -2<sup>31</sup> <= val <= 2<sup>31</sup> - 1
- Methods pop, top and getMin operations will always be called on non-empty stacks.
- At most 3 * 10<sup>4</sup> calls will be made to push, pop, top, and getMin.

## Tags
- stack

## Approach
**Key idea:** Keep a second stack whose top is always the minimum of the main stack; it only changes when a new minimum is pushed or the current minimum is popped.

1. `push(val)`: append to `stack`; also append to `min_stack` if it is empty or `val <= min_stack[-1]` (`<=` keeps duplicate minimums).
2. `pop()`: if the popped value equals `min_stack[-1]`, pop `min_stack` too.
3. `top()`: return `stack[-1]`.
4. `getMin()`: return `min_stack[-1]`.

## Code Implementation
```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []

    def push(self, val: int) -> None:
        self.stack.append(val)
        if not self.min_stack or val <= self.min_stack[-1]:
            self.min_stack.append(val)

    def pop(self) -> None:
        if self.stack[-1] == self.min_stack[-1]:
            self.min_stack.pop()
        self.stack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.min_stack[-1]
```

## Time Complexity Analysis
> Time complexity  : O(1) for all operations
>
> Space complexity : O(n)

## Related Problems
- [716. Max Stack](./716_max_stack.md) — 🔴 Hard · harder variant that also pops the max element
- [232. Implement Queue using Stacks](./232_implement_queue_using_stacks.md) — 🟢 Easy · auxiliary-stack design
- [1381. Design a Stack With Increment Operation](./1381_design_a_stack_with_increment_operation.md) — 🟡 Medium · augmenting a stack with extra O(1) operations
- [895. Maximum Frequency Stack](./895_maximum_frequency_stack.md) — 🔴 Hard · stack design with tracked statistics
