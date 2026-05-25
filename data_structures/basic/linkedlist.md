# Linked List

A linked list is a sequence of nodes where each node holds a value and a pointer to the next. Unlike arrays, insertions and deletions can be O(1) at any position (given a reference), without shifting elements.

## Complexity

| Operation | Time |
|---|---|
| Access by index | O(n) |
| Insert / Delete at head | O(1) |
| Insert / Delete at tail | O(1) with tail pointer, O(n) otherwise |
| Insert / Delete in middle | O(n) to find position, O(1) to update links |
| Search | O(n) |

## Python Implementation

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def append(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return
        curr = self.head
        while curr.next:
            curr = curr.next
        curr.next = new_node

    def search(self, key):
        curr = self.head
        while curr:
            if curr.data == key:
                return True
            curr = curr.next
        return False

    def delete(self, key):
        if self.head and self.head.data == key:
            self.head = self.head.next
            return
        curr = self.head
        while curr and curr.data != key:
            prev, curr = curr, curr.next
        if curr:
            prev.next = curr.next
```

## Related LeetCode Questions

### Reversal
- [206. Reverse Linked List](../../leetcode_questions/206_reverse_linked_list.md)
- [92. Reverse Linked List II](../../leetcode_questions/92_reverse_linked_list_II.md)
- [25. Reverse Nodes in K-Group](../../leetcode_questions/25_reverse_nodes_in_k_group.md)

### Merge
- [2. Add Two Numbers](../../leetcode_questions/2_add_two_numbers.md)
- [445. Add Two Numbers II](../../leetcode_questions/445_add_two_numbers_II.md)
- [21. Merge Two Sorted Lists](../../leetcode_questions/21_merge_two_sorted_lists.md)
- [23. Merge k Sorted Lists](../../leetcode_questions/23_merge_k_sorted_lists.md)

### Cycle Detection
- [141. Linked List Cycle](../../leetcode_questions/141_linked_list_cycle.md)
- [142. Linked List Cycle II](../../leetcode_questions/142_linked_list_cycle.md)
- [287. Find the Duplicate Number](../../leetcode_questions/287_find_the_duplicate_number.md)
- [160. Intersection of Two Linked Lists](../../leetcode_questions/160_intersection_of_two_linked_lists.md)

### Deletion
- [203. Remove Linked List Elements](../../leetcode_questions/203_remove_linked_list_elements.md)
- [83. Remove Duplicates from Sorted List](../../leetcode_questions/83_remove_duplicates_from_sorted_list.md)
- [82. Remove Duplicates from Sorted List II](../../leetcode_questions/82_remove_duplicates_from_sorted_list_II.md)
- [19. Remove Nth Node From End of List](../../leetcode_questions/19_remove_Nth_node_from_end_of_list.md)
- [1171. Remove Zero Sum Consecutive Nodes from Linked List](../../leetcode_questions/1171_remove_zero_sum_consecutive_nodes_from_linkedlist.md)

### Other
- [234. Palindrome Linked List](../../leetcode_questions/234_palindrome_linked_list.md)
- [138. Copy List with Random Pointer](../../leetcode_questions/138_copy_list_with_random_pointer.md)
- [426. Convert Binary Search Tree to Sorted Doubly Linked List](../../leetcode_questions/426_convert_binary_search_tree_to_sorted_doubly_linked_list.md)
