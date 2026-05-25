# 912. Sort an Array

## Question link
(https://leetcode.com/problems/sort-an-array/)

## Question Description
Given an array of integers nums, sort the array in ascending order.

Example 1:
> Input: nums = [5,2,3,1]
> Output: [1,2,3,5]

Example 2:
> Input: nums = [5,1,1,2,0,0]
> Output: [0,0,1,1,2,5]

Constraints:
1 <= nums.length <= 5 * 10<sup>4</sup> 
-5 * 10<sup>4</sup>  <= nums[i] <= 5 * 10<sup>4</sup> 

## Tags
- heap sort

## Code Implementation
```python
class Solution:
    def sortArray(self, nums: list[int]) -> list[int]:
        def heapify(arr: list[int], n: int, i: int) -> None:
            largest = i
            left = 2 * i + 1
            right = 2 * i + 2

            if left < n and arr[left] > arr[largest]:
                largest = left
            if right < n and arr[right] > arr[largest]:
                largest = right

            if largest != i:
                arr[i], arr[largest] = arr[largest], arr[i]
                heapify(arr, n, largest)

        n = len(nums)

        for i in range(n // 2, -1, -1):
            heapify(nums, n, i)

        for i in range(n - 1, 0, -1):
            nums[0], nums[i] = nums[i], nums[0]
            heapify(nums, i, 0)

        return nums
```

## Time Complexity Analysis
> Time complexity  : O(n log n)
>
> Space complexity : O(1)
