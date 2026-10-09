# 207. Course Schedule

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/course-schedule/)

## Question Description
There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return true if you can finish all courses. Otherwise, return false.

Example 1:
> Input: numCourses = 2, prerequisites = [[1,0]]
>
> Output: true
>
> Explanation: There are a total of 2 courses to take. 
>
> To take course 1 you should have finished course 0. So it is possible.

Example 2:
> Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
>
> Output: false
>
> Explanation: There are a total of 2 courses to take. 
>
> To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
 

Constraints:
- 1 <= numCourses <= 10<sup>5</sup>
- 0 <= prerequisites.length <= 5000
- prerequisites[i].length == 2
- 0 <= ai, bi < numCourses
- All the pairs prerequisites[i] are unique.

<br/>

## Tags
- graph
- topologic sort

## Approach
**Key idea:** All courses can be finished exactly when the prerequisite graph (`b -> a`) has no cycle, which a topological sort detects.

1. Build an adjacency list `pre -> course`.
2. **BFS (Kahn's):** count each node's indegree and queue every course with indegree 0.
3. Pop a course, count it as taken, and decrement its neighbours' indegrees, queueing any that reach 0.
4. If every course was taken there is no cycle; otherwise some courses are stuck on a cycle.
5. **DFS:** colour nodes unvisited / on-path / done; reaching an on-path node means a cycle.

## Code Implementation
### Approach 1: BFS (Kahn's algorithm)

```python
from collections import deque


class Solution:
    def canFinish(self, numCourses: int, prerequisites: list[list[int]]) -> bool:
        graph: list[list[int]] = [[] for _ in range(numCourses)]
        indegree = [0] * numCourses
        for course, pre in prerequisites:
            graph[pre].append(course)
            indegree[course] += 1

        q = deque(i for i in range(numCourses) if indegree[i] == 0)
        taken = 0
        while q:
            cur = q.popleft()
            taken += 1
            for nxt in graph[cur]:
                indegree[nxt] -= 1
                if indegree[nxt] == 0:
                    q.append(nxt)

        # Courses on a cycle never reach indegree 0
        return taken == numCourses
```

### Approach 2: DFS cycle detection

```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: list[list[int]]) -> bool:
        graph: list[list[int]] = [[] for _ in range(numCourses)]
        for course, pre in prerequisites:
            graph[pre].append(course)

        # 0 = unvisited, 1 = on the current DFS path, 2 = fully explored
        state = [0] * numCourses

        def has_cycle(u: int) -> bool:
            state[u] = 1
            for v in graph[u]:
                if state[v] == 1:  # back edge -> cycle
                    return True
                if state[v] == 0 and has_cycle(v):
                    return True
            state[u] = 2
            return False

        return not any(state[i] == 0 and has_cycle(i) for i in range(numCourses))
```

## Time Complexity Analysis
> Time complexity  : O(V + E) — V = numCourses, E = len(prerequisites)
>
> Space complexity : O(V + E) — adjacency list plus queue / recursion stack

## Related Problems
- [210. Course Schedule II](./210_course_schedule_ii.md) — 🟡 Medium · return the topological order itself
- [269. Alien Dictionary](./269_alien_dictionary.md) — 🔴 Hard · build a graph, then topological sort
- [261. Graph Valid Tree](./261_graph_valid_tree.md) — 🟡 Medium · cycle detection on an undirected graph
