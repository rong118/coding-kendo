# Graph Search

Searching in a graph data structure involves finding all nodes that satisfy certain conditions. 

## I. Breadth-First Search (BFS)

BFS starts at a given node and explores all its neighbors before moving on to the next level of nodes. It's useful for finding the shortest path between two nodes.

### Python Implementation
```python
class Node:
    def __init__(self, val):
        self.val = val
        self.neighbors = []

def bfs(start):
    # Initialize the queue with the starting node
    queue = [start]

    # Initialize the visited set
    visited = set()
    visited.add(start)

    # Loop until the queue is empty
    while queue:
        # Dequeue a node from the front of the queue
        node = queue.pop(0)

        # Process the current node
        print(node.val)

        # Enqueue all unvisited neighbors
        for neighbor in node.neighbors:
            if neighbor not in visited:
                queue.append(neighbor)
                visited.add(neighbor)

# Main code
if __name__ == "__main__":
    # Create nodes
    num_nodes = 6
    nodes = [Node(i) for i in range(num_nodes)]

    # Define neighbors
    nodes[0].neighbors.extend([nodes[1], nodes[2]])
    nodes[1].neighbors.extend([nodes[3]])
    nodes[2].neighbors.extend([nodes[4]])
    nodes[4].neighbors.extend([nodes[5]])

    # Run BFS from node 0
    bfs(nodes[0])
```

## II. Depth-First Search (DFS)

DFS also starts at a given node and explores as far as possible along each branch before backtracking.

### Python Implementation
```python
class Node:
    def __init__(self, val):
        self.val = val
        self.neighbors = []

def dfs(start, num_nodes):
    # Initialize the stack and visited list
    stack = [start]
    visited = [False] * num_nodes

    visited[start.val] = True

    while stack:
        # Pop a node from the stack
        node = stack.pop()

        # Process the current node
        print(node.val, end=" ")

        # Visit all unvisited neighbors
        for neighbor in node.neighbors:
            if not visited[neighbor.val]:
                stack.append(neighbor)
                visited[neighbor.val] = True

# Main code
if __name__ == "__main__":
    num_nodes = 6
    nodes = [Node(i) for i in range(num_nodes)]

    # Define neighbors
    nodes[0].neighbors.extend([nodes[1], nodes[2]])
    nodes[1].neighbors.extend([nodes[3]])
    nodes[2].neighbors.extend([nodes[4]])
    nodes[4].neighbors.extend([nodes[5]])

    # Run DFS from node 0
    dfs(nodes[0], num_nodes)
```

## III. Runtime Complexity
### Using an Adjacency List

When a graph is represented using an adjacency list, the runtime complexity of BFS is **O(V + E)**,
V is the number of vertices (nodes) in the graph. E is the number of edges in the graph.

It is because each vertex is visited at most once, leading to O(V) operations for vertices.
Each edge is considered once when exploring the neighbors of a vertex, leading to O(E) operations for edges.
Thus, the total time complexity is **O(V + E)**.

### Using an Adjacency Matrix

When a graph is represented using an adjacency matrix, the runtime complexity of BFS is **O(V^2)**. This is because:

Each vertex is visited at most once, leading to O(V) operations for vertices. **Checking all possible neighbors for each vertex requires O(V) time**, resulting in **O(V^2)** operations to explore all edges.

### Summary

DFS Time Complexity: **O(V + E)** or **O(V^2)**

BFS Time Complexity: **O(V + E)** or **O(V^2)**

DFS Space Complexity: **O(V)**

BFS Space Complexity: **O(V)**

## Leetcode Questions

| # | Problem | Difficulty |
|---|---------|------------|
| 127 | [Word Ladder](https://leetcode.com/problems/word-ladder/) | Hard |
| 130 | [Surrounded Regions](https://leetcode.com/problems/surrounded-regions/) | Medium |
| 133 | [Clone Graph](https://leetcode.com/problems/clone-graph/) | Medium |
| 200 | [Number of Islands](https://leetcode.com/problems/number-of-islands/) | Medium |
| 417 | [Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/) | Medium |
| 797 | [All Paths From Source to Target](https://leetcode.com/problems/all-paths-from-source-to-target/) | Medium |
| 994 | [Rotting Oranges](https://leetcode.com/problems/rotting-oranges/) | Medium |
