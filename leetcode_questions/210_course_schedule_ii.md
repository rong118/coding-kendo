# 210. Course Schedule II

**Difficulty:** 🟡 Medium

## Question link
(https://leetcode.com/problems/course-schedule-ii/)

## Question Description
There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return the ordering of courses you should take to finish all courses. If there are many valid answers, return any of them. If it is impossible to finish all courses, return an empty array.

<br/>

Example 1:
> Input: numCourses = 2, prerequisites = [[1,0]]
>
> Output: [0,1]
>
> Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1].

Example 2:
> Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
>
> Output: [0,2,1,3]
>
> Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.
>
> So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3].

Example 3:
> Input: numCourses = 1, prerequisites = []
>
> Output: [0]

Constraints:
- 1 <= numCourses <= 2000
- 0 <= prerequisites.length <= numCourses * (numCourses - 1)
- prerequisites[i].length == 2
- 0 <= ai, bi < numCourses
- ai != bi
- All the pairs [ai, bi] are distinct.

## Tags
- graph
- topologic sort

## Approach
**Key idea:** A valid course order is a topological sort of the prerequisite graph; if the graph has a cycle, no order exists.

1. Build a graph with an edge `prerequisite -> course` and count each course's indegree.
2. BFS (Kahn's algorithm): queue every course with indegree 0, pop one at a time into the answer, and decrement its neighbors' indegrees, queueing any that reach 0.
3. If fewer than `numCourses` courses were output, there is a cycle, so return `[]`.
4. DFS alternative: color nodes unvisited / visiting / done; reaching a "visiting" node means a cycle. Add each node after all its dependents (post-order) and reverse the list at the end.

## Code Implementation
### Approach 1: BFS (Kahn's algorithm)

```python
from collections import defaultdict, deque


class Solution:
    def findOrder(self, numCourses: int, prerequisites: list[list[int]]) -> list[int]:
        graph = defaultdict(list)
        indegree = [0] * numCourses
        for course, pre in prerequisites:
            graph[pre].append(course)
            indegree[course] += 1

        q = deque(i for i in range(numCourses) if indegree[i] == 0)
        order = []
        while q:
            cur = q.popleft()
            order.append(cur)
            for nxt in graph[cur]:
                indegree[nxt] -= 1
                if indegree[nxt] == 0:
                    q.append(nxt)

        # Some courses never reached indegree 0 -> cycle
        return order if len(order) == numCourses else []
```

### Approach 2: DFS

```python
class Solution:
    def findOrder(self, numCourses: int, prerequisites: list[list[int]]) -> list[int]:
        graph = [[] for _ in range(numCourses)]
        for course, pre in prerequisites:
            graph[pre].append(course)

        # 0 = unvisited, 1 = visiting (on the stack), 2 = done
        state = [0] * numCourses
        order = []
        valid = True

        def dfs(u: int) -> None:
            nonlocal valid
            state[u] = 1
            for v in graph[u]:
                if state[v] == 0:
                    dfs(v)
                elif state[v] == 1:
                    valid = False  # back edge -> cycle
            state[u] = 2
            order.append(u)  # post-order: u comes after all courses that depend on it

        for i in range(numCourses):
            if state[i] == 0:
                dfs(i)

        return order[::-1] if valid else []
```

## Time Complexity Analysis
> Time complexity  : O(V + E) — V = numCourses, E = len(prerequisites); each node and edge is processed once
>
> Space complexity : O(V + E) — adjacency list, plus the queue / recursion stack

## Related Problems
- [207. Course Schedule](./207_course_schedule.md) — 🟡 Medium · same graph, only asks whether an order exists
- [269. Alien Dictionary](./269_alien_dictionary.md) — 🔴 Hard · topological sort on letters
- [2127. Maximum Employees to Be Invited to a Meeting](./2127_maximum_employees_to_be_invited_to_a_meeting.md) — 🔴 Hard · Kahn-style peeling of a dependency graph
