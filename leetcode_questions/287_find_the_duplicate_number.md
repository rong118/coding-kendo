# 287. Find the Duplicate Number

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/find-the-duplicate-number/)

## Question Description
Given an array of integers nums containing n + 1 integers where each integer is in the range [1, n] inclusive.

There is only one repeated number in nums, return this repeated number.

You must solve the problem without modifying the array nums and uses only constant extra space.

Example 1:
> Input: nums = [1,3,4,2,2]
> 
> Output: 2

Example 2:
> Input: nums = [3,1,3,4,2]
> Output: 3

Example 3:
> Input: nums = [1,1]
>
> Output: 1

Example 4:
> Input: nums = [1,1,2]
>
> Output: 1

Constraints:
- 1 <= n <= 10<sup>5</sup> 
- nums.length == n + 1
- 1 <= nums[i] <= n
- All the integers in nums appear only once except for precisely one integer which appears two or more times.

## Tags
- hashmap
- array
- fast slow pointer

## Approach
**Key idea:** Treat the array as a linked list where index `i` points to `nums[i]`. Values are in `[1, n]` but there are `n + 1` indices, so two indices point to the same node, which creates a cycle whose entrance is the duplicate. Floyd's tortoise and hare finds that entrance in O(n) time and O(1) space without changing the array.

1. Simple options first: sort and compare neighbors, or use a hash set. These break the rules (they change the array or use extra space).
2. Negative marking: for each value `x`, flip the sign of `nums[x - 1]`; if it is already negative, `x` is the duplicate. This also changes the array.
3. Floyd phase 1: move `slow` one step (`nums[slow]`) and `fast` two steps (`nums[nums[fast]]`) until they meet inside the cycle.
4. Floyd phase 2: reset one pointer to the start and move both one step at a time; they meet at the cycle entrance, which is the duplicate.

## Code Implementation
### Approach 1: Sorting

```python
class Solution:
    def findDuplicate(self, nums: list[int]) -> int:
        nums.sort()  # in place (mutates the input)
        for i in range(1, len(nums)):
            if nums[i] == nums[i - 1]:
                return nums[i]
        return -1
```

### Approach 2: Hash set

```python
class Solution:
    def findDuplicate(self, nums: list[int]) -> int:
        seen = set()
        for x in nums:
            if x in seen:
                return x
            seen.add(x)
        return -1
```

### Approach 3: Negative marking

```python
class Solution:
    def findDuplicate(self, nums: list[int]) -> int:
        for x in nums:
            idx = abs(x) - 1
            if nums[idx] < 0:  # already marked -> seen before
                return idx + 1
            nums[idx] = -nums[idx]
        return -1
```

### Approach 4: Fast & slow pointers (Floyd's cycle detection)

<img src="../resources/assets/lc287.png" width="400" />

```python
class Solution:
    def findDuplicate(self, nums: list[int]) -> int:
        # Phase 1: find a meeting point inside the cycle
        slow = fast = nums[0]
        while True:
            slow = nums[slow]
            fast = nums[nums[fast]]
            if slow == fast:
                break

        # Phase 2: the entrance of the cycle is the duplicate
        fast = nums[0]
        while slow != fast:
            slow = nums[slow]
            fast = nums[fast]
        return slow
```

## Time Complexity Analysis
> Time complexity  : O(n) — fast & slow pointers (also hash set and negative marking); sorting is O(n log n)
>
> Space complexity : O(1) — fast & slow pointers, without changing the array (hash set: O(n); sorting and negative marking: O(1) but they change the input)

## Related Problems
- [142. Linked List Cycle II](./142_linked_list_cycle_II.md) — 🟡 Medium · the same Floyd's cycle-entrance technique
- [448. Find All Numbers Disappeared in an Array](./448_find_all_numbers_disappeared_in_an_array.md) — 🟢 Easy · negative-marking on values in `[1, n]`
- [41. First Missing Positive](https://leetcode.com/problems/first-missing-positive) — 🔴 Hard · uses the array itself as a hash table
- [217. Contains Duplicate](./217_contain_duplicate.md) — 🟢 Easy · duplicate detection with a hash set
