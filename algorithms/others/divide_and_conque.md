# Divide And Conque

The Divide and Conquer algorithm is a problem-solving approach that breaks a problem down into smaller subproblems, solves each subproblem independently, and then combines the solutions to solve the original problem. 

This method is particularly useful for tasks that can be naturally divided into smaller, similar tasks, and it often leads to efficient and elegant solutions.

## Steps in Divide and Conquer

1. Divide: Break the problem into smaller subproblems.
2. Conquer: Solve the subproblems recursively. If the subproblem is small enough, solve it directly.
3. Combine: Combine the solutions of the subproblems to form the solution of the original problem.

## Examples

### 1. MergeSort

Merge Sort is a classic example of a Divide and Conquer algorithm:

```python
def merge(arr: list[int], left: int, mid: int, right: int) -> None:
    left_arr = arr[left:mid + 1]
    right_arr = arr[mid + 1:right + 1]

    # Merge the two sorted halves back into arr[left..right]
    i = j = 0
    k = left
    while i < len(left_arr) and j < len(right_arr):
        if left_arr[i] <= right_arr[j]:
            arr[k] = left_arr[i]
            i += 1
        else:
            arr[k] = right_arr[j]
            j += 1
        k += 1

    # Copy whatever remains in either half
    for x in left_arr[i:] + right_arr[j:]:
        arr[k] = x
        k += 1


def merge_sort(arr: list[int], left: int, right: int) -> None:
    if left < right:
        mid = (left + right) // 2
        merge_sort(arr, left, mid)       # Sort first half
        merge_sort(arr, mid + 1, right)  # Sort second half
        merge(arr, left, mid, right)     # Merge the sorted halves


arr = [12, 11, 13, 5, 6, 7]
print("Given array is", arr)
merge_sort(arr, 0, len(arr) - 1)
print("Sorted array is", arr)  # [5, 6, 7, 11, 12, 13]
```

### 2. Finding the maximum and minimum elements in an array:

```python
def find_min_max(arr: list[int], left: int, right: int) -> tuple[int, int]:
    # If the array has only one element
    if left == right:
        return arr[left], arr[left]

    # If the array has two elements
    if right == left + 1:
        return min(arr[left], arr[right]), max(arr[left], arr[right])

    # Divide the array into two halves
    mid = (left + right) // 2
    left_min, left_max = find_min_max(arr, left, mid)
    right_min, right_max = find_min_max(arr, mid + 1, right)

    # Combine the results
    return min(left_min, right_min), max(left_max, right_max)


arr = [100, 11, 445, 1, 330, 3000]
lo, hi = find_min_max(arr, 0, len(arr) - 1)
print("Minimum element is", lo)  # 1
print("Maximum element is", hi)  # 3000
```

## Runtime Complexity

The runtime complexity of a Divide and Conquer algorithm can vary depending on how the problem is divided and how the solutions are combined.

Generally, it can be relations of the form:

T(n) = a * T(b/n) + f(n)

- T(n) is the time complexity of the algorithm.
- a is the number of subproblems into which the problem is divided.
- n/b is the size of each subproblem.
- f(n) is the cost of dividing the problem and combining the results of the subproblems.

For example, The recurrence relation for Merge Sort is: 

T(n) = 2 * T(2 * n) + O(n)

After applying the Master Theorem, T(n) = O(nlogn)