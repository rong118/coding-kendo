# Common Runtime CheatSheet

## Data Structure Operations Complexity

| Data Structure          | Access    | Search    | Insertion | Deletion  | Comments  |
| ----------------------- | :-------: | :-------: | :-------: | :-------: | :-------- |
| **Array**               | O(1)      | O(n)      | O(n)      | O(n)      |           |
| **Stack**               | O(n)      | O(n)      | O(1)      | O(1)      |           |
| **Queue**               | O(n)      | O(n)      | O(1)      | O(1)      |           |
| **Linked List**         | O(n)      | O(n)      | O(1)      | O(n)      |           |
| **Hash Table**          | -         | O(1)*     | O(1)*     | O(1)*     | *Average; O(n) worst-case |
| **Binary Search Tree**  | O(n)      | O(n)      | O(n)      | O(n)      | O(log n) when balanced |
| **B-Tree**              | O(log n)  | O(log n)  | O(log n)  | O(log n)  |           |
| **Red-Black Tree**      | O(log n)  | O(log n)  | O(log n)  | O(log n)  |           |
| **AVL Tree**            | O(log n)  | O(log n)  | O(log n)  | O(log n)  |           |
| **Bloom Filter**        | -         | O(1)      | O(1)      | -         | May return false positives |

## Array Sorting Algorithms Complexity

| Name                  | Best            | Average             | Worst               | Memory    | Stable | Comments  |
| --------------------- | :-------------: | :-----------------: | :-----------------: | :-------: | :----: | :-------- |
| **Bubble sort**       | O(n)            | O(n²)               | O(n²)               | O(1)      | Yes    |           |
| **Insertion sort**    | O(n)            | O(n²)               | O(n²)               | O(1)      | Yes    |           |
| **Selection sort**    | O(n²)           | O(n²)               | O(n²)               | O(1)      | No     |           |
| **Heap sort**         | O(n log n)      | O(n log n)          | O(n log n)          | O(1)      | No     |           |
| **Merge sort**        | O(n log n)      | O(n log n)          | O(n log n)          | O(n)      | Yes    |           |
| **Quick sort**        | O(n log n)      | O(n log n)          | O(n²)               | O(log n)  | No     | In-place; O(log n) stack space |
| **Shell sort**        | O(n log n)      | depends on gap      | O(n (log n)²)       | O(1)      | No     |           |
| **Counting sort**     | O(n + r)        | O(n + r)            | O(n + r)            | O(n + r)  | Yes    | r = max value in array |
| **Radix sort**        | O(n · k)        | O(n · k)            | O(n · k)            | O(n + k)  | Yes    | k = length of longest key |
