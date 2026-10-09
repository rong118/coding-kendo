# Brute Force

Brute Force Algorithm is a simple algorithmic approach to solve problems. It's based on the idea of trying all possible solutions until you find the correct one.

## I. Workflow
1. Tries every possible solution: The algorithm systematically checks each possibility, no matter how many there are.
2. Does not use any heuristics or shortcuts: Unlike other algorithms, Brute Force doesn't rely on clever tricks or rules of thumb to reduce the number of possibilities to consider.
3. Eventually finds a correct solution (if one exists): By trying every possible solution, the algorithm will eventually find a valid answer if one exists.

## II. Example
### Python Implementation
Below is an example of finding all possible permutations of a string.
```python
def print_permutations(chars: list[str], l: int) -> None:
    if l == len(chars) - 1:
        print("".join(chars))
        return
    for i in range(l, len(chars)):
        chars[l], chars[i] = chars[i], chars[l]
        print_permutations(chars, l + 1)
        chars[l], chars[i] = chars[i], chars[l]  # backtrack


print_permutations(list("abc"), 0)  # abc acb bac bca cba cab
```

##  III. Drawbacks

While Brute Force Algorithms can be effective, they often have significant drawbacks:
- Slow performance: The algorithm may take an impractically long time to complete, especially for large search spaces.
- High computational cost: The algorithm's resource usage (e.g., CPU cycles, memory) can be substantial.

## IV. Summary

Brute Force Algorithm is a simple, straightforward approach that tries every possible solution until it finds the correct one.

While effective in certain situations, it may not always be the most efficient or practical choice.
