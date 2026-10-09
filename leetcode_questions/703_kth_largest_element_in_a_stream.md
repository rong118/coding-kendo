# 703. Kth Largest Element in a Stream

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/kth-largest-element-in-a-stream/)

## Question Description
Design a class to find the `kth` largest element in a stream. Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Implement the `KthLargest` class:

* `KthLargest(int k, int[] nums)` Initializes the object with the integer `k` and the stream of integers `nums`.
* `int add(int val)` Appends the integer `val` to the stream and returns the element representing the `kth` largest element in the stream.

Example 1:

> Input
> ["KthLargest", "add", "add", "add", "add", "add"]
> [[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]
> Output
> [null, 4, 5, 5, 8, 8]
>
> Explanation
> KthLargest kthLargest = new KthLargest(3, [4, 5, 8, 2]);
> kthLargest.add(3);   // return 4
> kthLargest.add(5);   // return 5
> kthLargest.add(10);  // return 5
> kthLargest.add(9);   // return 8
> kthLargest.add(4);   // return 8

Constraints:

* 1 <= k <= 10^4
* 0 <= nums.length <= 10^4
* -10^4 <= nums[i] <= 10^4
* -10^4 <= val <= 10^4
* At most 10^4 calls will be made to `add`.
* It is guaranteed that there will be at least `k` elements in the array when you search for the `kth` element.

## Tags
- heap

## Approach
**Key idea:** Keep a min-heap of only the `k` largest values seen so far; its root is then always the `k`th largest element of the stream.

1. Store `k` and start with an empty min-heap.
2. Feed every initial number through `add`.
3. In `add`, push the new value onto the heap.
4. If the heap has more than `k` elements, pop the smallest.
5. Return the heap root.

## Code Implementation
```python
import heapq

class KthLargest:
    def __init__(self, k: int, nums: list[int]):
        self.k = k
        self.heap = []
        for num in nums:
            self.add(num)

    def add(self, val: int) -> int:
        heapq.heappush(self.heap, val)
        if len(self.heap) > self.k:
            heapq.heappop(self.heap)  # evict the smallest among k+1
        return self.heap[0]
```

## Time Complexity Analysis
> Time complexity  : O(log k) per add — push/pop on a heap of size ≤ k
>
> Space complexity : O(k) — the heap holds at most k elements

## Related Problems
- [215. Kth Largest Element in an Array](./215_kth_largest_element_in_an_array.md) — 🟡 Medium · same size-k heap on a static array
- [295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream) — 🔴 Hard · order statistics on a stream with heaps
- [347. Top K Frequent Elements](./347_top_k_frequent_elements.md) — 🟡 Medium · size-k heap selection
