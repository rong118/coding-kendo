# Topological Sort

Topological sorting is a linear ordering of vertices in a **directed acyclic graph (DAG)** such that for every directed edge u→v, vertex u comes before v in the ordering.

## key characteristics

### - Ordering:

TS produces a linear ordering of the vertices in a directed acyclic graph (DAG), such that for every edge (u, v), vertex u comes before vertex v in the ordering.

### - No Cycles:

TS only works on DAGs, meaning there are no cycles in the graph. If a cycle is present, the algorithm will not be able to produce a valid topological ordering.

### - Not Necessarily Unique:

TS may not always produce a unique ordering for a given graph. This is because there may be multiple valid topological orderings for a graph that has multiple DAGs as subgraphs.

### - Can Be Used for Scheduling:

One of the most common applications of Topological Sort is in scheduling, where it can be used to schedule tasks or jobs based on their dependencies.

## Using Depth-First Search (DFS) 

### Python Implementation

```python
from collections import defaultdict

def topological_sort_dfs(vertices, edges):
    # Step 1: Build the graph
    graph = defaultdict(list)
    for src, dest in edges:
        graph[src].append(dest)
    
    # Step 2: Initialize visited set and stack
    visited = set()
    stack = []

    # Step 3: Recursive function to perform DFS
    def dfs(node):
        visited.add(node)
        for neighbor in graph[node]:
            if neighbor not in visited:
                dfs(neighbor)
        # Push the node onto the stack after all its neighbors are visited
        stack.append(node)

    # Step 4: Perform DFS for all unvisited nodes
    for vertex in range(vertices):
        if vertex not in visited:
            dfs(vertex)
    
    # Step 5: Reverse the stack to get the topological order
    return stack[::-1]

# Example usage
vertices = 6
edges = [
    (5, 2),
    (5, 0),
    (4, 0),
    (4, 1),
    (2, 3),
    (3, 1)
]

print("Topological Sort:", topological_sort_dfs(vertices, edges))
```

## Kahn's algorithm

Kahn's algorithm is a method for performing topological sorting on a directed acyclic graph (DAG) by using Breath First Search (BFS).

### Python Implementation
```python
from collections import defaultdict, deque

def kahns_algorithm(vertices, edges):
    # Step 1: Build the graph and calculate in-degrees
    in_degree = {i: 0 for i in range(vertices)}  # Initialize in-degree for each node
    graph = defaultdict(list)  # Adjacency list representation

    for src, dest in edges:
        graph[src].append(dest)
        in_degree[dest] += 1

    # Step 2: Collect nodes with in-degree of 0
    queue = deque([node for node in in_degree if in_degree[node] == 0])
    topological_order = []

    # Step 3: Process the graph
    while queue:
        current = queue.popleft()
        topological_order.append(current)

        # Reduce the in-degree of each neighbor
        for neighbor in graph[current]:
            in_degree[neighbor] -= 1
            # If in-degree becomes 0, add to queue
            if in_degree[neighbor] == 0:
                queue.append(neighbor)

    # Step 4: Check for cycles
    if len(topological_order) != vertices:
        return "Graph has a cycle. Topological sorting not possible."

    return topological_order

# Example usage
vertices = 6
edges = [
    (5, 2),
    (5, 0),
    (4, 0),
    (4, 1),
    (2, 3),
    (3, 1)
]

print("Topological Sort:", kahns_algorithm(vertices, edges))
```

## Runtime Complexity:

### - Depth-First Search (DFS) Based Topological Sort

Each vertex is visited exactly once, marking it as visited. This contributes **O(V)** to the complexity.
For each vertex, all its adjacent vertices (edges) are explored. This traversal of all edges contributes **O(E)** to the complexity.
Thus, the total complexity for the DFS-based topological sort is **O(V+E)**.

### - Kahn's algorithm

The time complexity of Kahn's algorithm is **O(V+E)**, where V is the number of vertices and E is the number of edges in the graph. 

This is because each vertex and each edge is processed exactly once.

## Leetcode Questions

| # | Problem | Difficulty |
|---|---------|------------|
| 207 | [Course Schedule](../../leetcode_questions/207_course_schedule.md) | Medium |
| 210 | [Course Schedule II](../../leetcode_questions/210_course_schedule_ii.md) | Medium |
| 269 | [Alien Dictionary](../../leetcode_questions/269_alien_dictionary.md) | Hard |
| 2127 | [Maximum Employees to Be Invited to a Meeting](../../leetcode_questions/2127_maximum_employees_to_be_invited_to_a_meeting.md) | Hard |
