# Binary Index Tree

A Binary Indexed Tree (BIT) is a data structure used to efficiently calculate prefix sums and cumulative values of an array or vector.

## How BIT works:

- **Initialization**: Create an array BIT with the same length as the original array, initialized to zero.

- **Insert**: When updating an element at index i, calculate the prefix sum from 0 to i-1 and store it in BIT[i].

- **Query**: To compute the cumulative sum from start to end, traverse the BIT from BIT[start-1] to BIT[end]. The key insight is that you can skip certain nodes by using binary indexing (bit manipulation) to determine whether a node should be included in the sum or not.

## Implementation
```python
class BIT:
    def __init__(self, n):
        self.bit = [0] * (n + 1)

    def update(self, i, val):
        while i < len(self.bit):
            self.bit[i] += val
            i += i & -i

    def query(self, i):
        total = 0
        while i > 0:
            total += self.bit[i]
            i -= i & -i
        return total

# Main code
bit = BIT(10)  # Initialize a BIT of size 10

arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]  # Example array

for i in range(len(arr)):
    bit.update(i + 1, arr[i])  # Update the BIT with the values from the array (1-based index)

print("Cumulative sum from index 2 to 5:", bit.query(5) - bit.query(1))  # Calculate the cumulative sum for the range [2, 5]
```

### Binary searching by i & -i

In the Go code, the line for ; i > 0; i -= i & -i { ... } is a loop that iterates through the bits of the index i.

- i & -i is a bitwise operation that finds the highest bit set in i. In binary, this would be equivalent to finding the most significant 1 bit.

- i -= i & -i updates the value of i by subtracting the highest bit set in i. This effectively "moves" the loop to the next least significant bit.

This technique is called "**bit twiddling**" or "**binary searching**", and it's used to efficiently iterate through the bits of an integer. By repeatedly updating i to the next lowest bit, we can traverse the binary representation of i from most significant bit to least significant bit.

In the context of the BIT implementation, this loop is used in both the Update and Query methods to efficiently calculate the cumulative sum or update the BIT values.

## Runtime Complexity

The runtime complexity of a Binary Indexed Tree (BIT) depends on the operation being performed:

### - Update

The update operation has an average-case time complexity of O(log n), where n is the size of the BIT. This is because we only need to traverse the BIT up to the highest bit set in the updated index.

### - Query

The query operation has an average-case time complexity of O(log n) as well, since we need to traverse the BIT from the highest bit set in the start index down to the lowest bit set in the end index.

## LeetCode Questions

| # | Problem | Difficulty |
|---|---------|------------|
| 307 | [Range Sum Query - Mutable](https://leetcode.com/problems/range-sum-query-mutable/) | Medium |
| 308 | [Range Sum Query 2D - Mutable](https://leetcode.com/problems/range-sum-query-2d-mutable/) | Medium |
| 315 | [Count of Smaller Numbers After Self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/) | Hard |
| 327 | [Count of Range Sum](https://leetcode.com/problems/count-of-range-sum/) | Hard |
| 440 | [K-th Smallest in Lexicographical Order](https://leetcode.com/problems/k-th-smallest-in-lexicographical-order/) | Hard |
