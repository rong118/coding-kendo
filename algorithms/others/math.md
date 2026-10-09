# Math Topics

## 1. Greatest Common Divisor

The Greatest Common Divisor (GCD) of two or more integers is the largest positive integer that divides each of the integers without leaving a remainder. For example, the GCD of 8 and 12 is 4.

One of the most efficient algorithms to compute the GCD is the Euclidean algorithm. The Euclidean algorithm is based on the principle that the GCD of two numbers a and b (where a>b) is the same as the GCD of 
b and (a mod b).

### Implementation
```python
def gcd(a: int, b: int) -> int:
    """Return the GCD of two numbers using the Euclidean algorithm."""
    while b != 0:
        a, b = b, a % b
    return a


print(gcd(8, 12))  # 4
```

### LeetCode

- [1979. Find Greatest Common Divisor of Array](../../leetcode_questions/1979_find_greatest_common_divisor.md)