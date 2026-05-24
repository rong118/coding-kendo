# Big O Notation

Big O notation describes how an algorithm's time or space requirements grow as the input size (n) increases.

## Key Points
- **Growth rate**: Big O cares about how performance scales with large n, not absolute speed.
- **Worst-case**: It measures the upper bound — the most time/space an algorithm could need.
- **Constants ignored**: O(2n) and O(n) are equivalent; only the dominant term matters (e.g., O(n² + n) = O(n²)).

## Growth Order (fastest to slowest)

`O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ) < O(n!)`

## Common Complexities

| Big O Notation | n = 10 | n = 100 | n = 1000 | Common Pattern |
| :--- | ---: | ---: | ---: | :--- |
| **O(1)**       | 1 | 1 | 1 | Direct access (array index, hash table lookup) |
| **O(log n)**   | ~3 | ~7 | ~10 | Halving the problem each step (binary search) |
| **O(n)**       | 10 | 100 | 1000 | Single loop through input |
| **O(n log n)** | ~33 | ~664 | ~9966 | Divide & conquer sorting (merge sort, quick sort) |
| **O(n²)**      | 100 | 10000 | 1000000 | Nested loops over input |
| **O(2ⁿ)**      | 1024 | ~1.3e30 | ~1e301 | Trying all subsets (brute force combinations) |
| **O(n!)**      | 3.6e6 | ~9e157 | ~4e2568 | Trying all permutations |
