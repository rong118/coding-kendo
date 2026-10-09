# 622. Design Circular Queue

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/design-circular-queue/)

## Question Description
Design your implementation of the circular queue. The circular queue is a linear data structure in which the operations are performed based on FIFO (First In First Out) principle and the last position is connected back to the first position to make a circle. It is also called "Ring Buffer".

One of the benefits of the circular queue is that we can make use of the spaces in front of the queue. In a normal queue, once the queue becomes full, we cannot insert the next element even if there is a space in front of the queue. But using the circular queue, we can use the space to store new values.

Implement the `MyCircularQueue` class:

* `MyCircularQueue(k)` Initializes the object with the size of the queue to be `k`.
* `int Front()` Gets the front item from the queue. If the queue is empty, return `-1`.
* `int Rear()` Gets the last item from the queue. If the queue is empty, return `-1`.
* `boolean enQueue(int value)` Inserts an element into the circular queue. Return `true` if the operation is successful.
* `boolean deQueue()` Deletes an element from the circular queue. Return `true` if the operation is successful.
* `boolean isEmpty()` Checks whether the circular queue is empty or not.
* `boolean isFull()` Checks whether the circular queue is full or not.

You must solve the problem **without** using the built-in queue data structure in your programming language.

Example 1:

> Input
> ["MyCircularQueue", "enQueue", "enQueue", "enQueue", "enQueue", "Rear", "isFull", "deQueue", "enQueue", "Rear"]
> [[3], [1], [2], [3], [4], [], [], [], [4], []]
> Output
> [null, true, true, true, false, 3, true, true, true, 4]
>
> Explanation
> MyCircularQueue myCircularQueue = new MyCircularQueue(3);
> myCircularQueue.enQueue(1); // return True
> myCircularQueue.enQueue(2); // return True
> myCircularQueue.enQueue(3); // return True
> myCircularQueue.enQueue(4); // return False
> myCircularQueue.Rear();     // return 3
> myCircularQueue.isFull();   // return True
> myCircularQueue.deQueue();  // return True
> myCircularQueue.enQueue(4); // return True
> myCircularQueue.Rear();     // return 4

Constraints:

* 1 <= k <= 1000
* 0 <= value <= 1000
* At most 3000 calls will be made to `enQueue`, `deQueue`, `Front`, `Rear`, `isEmpty`, and `isFull`.

## Tags
- queue

## Approach
**Key idea:** Use a fixed array of size `k` with `front` and `rear` indices that wrap around using `% k`. A separate `size` counter tells empty and full apart.

1. Allocate `q = [0] * k`, with `front = 0`, `rear = -1`, and `size = 0`.
2. `enQueue`: if the queue is full, return `False`; otherwise move `rear` forward with wrap-around, store the value, and increase `size`.
3. `deQueue`: if the queue is empty, return `False`; otherwise move `front` forward with wrap-around and decrease `size`.
4. `Front` / `Rear` return `q[front]` / `q[rear]`, or `-1` when the queue is empty.
5. `isEmpty` is `size == 0` and `isFull` is `size == k`.

## Code Implementation
```python
class MyCircularQueue:
    def __init__(self, k: int):
        self.q = [0] * k
        self.front = 0
        self.rear = -1
        self.size = 0
        self.capacity = k

    def enQueue(self, value: int) -> bool:
        if self.isFull():
            return False
        self.rear = (self.rear + 1) % self.capacity
        self.q[self.rear] = value
        self.size += 1
        return True

    def deQueue(self) -> bool:
        if self.isEmpty():
            return False
        self.front = (self.front + 1) % self.capacity
        self.size -= 1
        return True

    def Front(self) -> int:
        return -1 if self.isEmpty() else self.q[self.front]

    def Rear(self) -> int:
        return -1 if self.isEmpty() else self.q[self.rear]

    def isEmpty(self) -> bool:
        return self.size == 0

    def isFull(self) -> bool:
        return self.size == self.capacity
```

## Time Complexity Analysis
> Time complexity  : O(1) for all operations
>
> Space complexity : O(k) — fixed-size array for ring buffer

## Related Problems
- [641. Design Circular Deque](./641_design_circular_deque.md) — 🟡 Medium · same ring buffer with both ends
- [232. Implement Queue using Stacks](./232_implement_queue_using_stacks.md) — 🟢 Easy · build a queue from other structures
- [225. Implement Stack using Queues](./225_implement_stack_using_queue.md) — 🟢 Easy · design a basic container
