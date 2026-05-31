# Heap

A heap is a complete binary tree where each parent is ordered relative to its children:
- **Min-Heap**: parent <= children
- **Max-Heap**: parent >= children

Heaps are typically implemented with arrays:
- `A[0]` is the root
- Left child of `A[i]` is `A[2*i + 1]`, right child is `A[2*i + 2]`

## Complexity

| Operation | Time |
|---|---|
| Push / Pop | O(log n) |
| Peek (root) | O(1) |
| Heapify (build) | O(n) |
| Heap Sort | O(n log n) |

## Python Usage

### heapq (min-heap)

```python
import heapq

nums = [3, 1, 4, 1, 5]
heapq.heapify(nums)           # in-place, O(n)
heapq.heappush(nums, 2)        # O(log n)
smallest = heapq.heappop(nums) # O(log n)
```

### Max-heap (negate values)

```python
max_heap = []
heapq.heappush(max_heap, -10)
largest = -heapq.heappop(max_heap)
```

### Priority Queue

```python
from queue import PriorityQueue

pq = PriorityQueue()
pq.put((2, "Task 2"))
pq.put((1, "Task 1"))
while not pq.empty():
    priority, task = pq.get()
```

## Related LeetCode Questions

| # | Problem | Technique |
|---|---------|-----------|
| 23 | [Merge k Sorted Lists](../../leetcode_questions/23_merge_k_sorted_lists.md) | Min-heap of k list heads |
| 215 | [Kth Largest Element in an Array](../../leetcode_questions/215_kth_largest_element_in_an_array.md) | Min-heap of size k for top-k selection |
| 347 | [Top K Frequent Elements](../../leetcode_questions/347_top_k_frequent_elements.md) | Min-heap of size k with frequency |
| 703 | [Kth Largest Element in a Stream](../../leetcode_questions/703_kth_largest_element_in_a_stream.md) | Streaming min-heap of size k |
