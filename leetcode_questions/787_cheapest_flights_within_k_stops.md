# 787. Cheapest Flights Within K Stops

**Difficulty:** 🟡 Medium

## Question link
> (https://leetcode.com/problems/cheapest-flights-within-k-stops/)

## Question Description
There are n cities connected by some number of flights. You are given an array flights where flights[i] = [fromi, toi, pricei] indicates that there is a flight from city fromi to city toi with cost pricei.

You are also given three integers src, dst, and k, return the cheapest price from src to dst with at most k stops. If there is no such route, return -1.

Example 1:
> <img src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/02/16/995.png" width="400" />
>
> Input: n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 1
>
> Output: 200
>
> Explanation: The graph is shown.
>
> The cheapest price from city 0 to city 2 with at most 1 stop costs 200, as marked red in the picture.


Example 2:
> <img src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/02/16/995.png" width="400" />
>
> Input: n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 0
> 
> Output: 500
>
> Explanation: The graph is shown.
>
> The cheapest price from city 0 to city 2 with at most 0 stop costs 500, as marked blue in the picture.

Constraints:
- 1 <= n <= 100
- 0 <= flights.length <= (n * (n - 1) / 2)
- flights[i].length == 3
- 0 <= fromi, toi < n
- fromi != toi
- 1 <= pricei <= 104
- There will not be any multiple flights between two cities.
- 0 <= src, dst, k < n
- src != dst

## Tags
- graph 
- dijkstra
- bellman-ford

## Approach
**Key idea:** At most `k` stops means at most `k + 1` flights, so the search state must include how many edges are left — either Dijkstra over `(city, stops left)` or Bellman-Ford limited to `k + 1` rounds.

1. **Dijkstra:** push `(cost, src, k)` into a min-heap and pop the cheapest state each time.
2. The first time `dst` is popped, its cost is the answer.
3. Skip a state if it has no stops left or the city was already expanded with at least as many stops remaining (that earlier visit was also cheaper); otherwise push every outgoing flight with `stops - 1`.
4. **Bellman-Ford:** run `k + 1` rounds; in each, relax every flight using a copy of the previous round's costs so a round extends paths by exactly one edge.
5. Return the cost of `dst`, or `-1` if it was never reached.

## Code Implementation
### Approach 1: Dijkstra with stop count

```python
import heapq


class Solution:
    def findCheapestPrice(self, n: int, flights: list[list[int]], src: int, dst: int, k: int) -> int:
        graph: list[list[tuple[int, int]]] = [[] for _ in range(n)]
        for u, v, price in flights:
            graph[u].append((v, price))

        # (cost so far, city, stops still allowed)
        heap = [(0, src, k)]
        best_stops = [-2] * n  # most stops left when each city was expanded
        while heap:
            cost, city, stops = heapq.heappop(heap)
            if city == dst:
                return cost
            if stops < 0 or stops <= best_stops[city]:
                continue  # out of stops, or already expanded cheaper with more stops left
            best_stops[city] = stops
            for nxt, price in graph[city]:
                heapq.heappush(heap, (cost + price, nxt, stops - 1))
        return -1
```

### Approach 2: Bellman-Ford

```python
class Solution:
    def findCheapestPrice(self, n: int, flights: list[list[int]], src: int, dst: int, k: int) -> int:
        INF = float("inf")
        cost = [INF] * n
        cost[src] = 0
        for _ in range(k + 1):  # k stops = at most k + 1 edges
            cur = cost[:]  # relax only from the previous round's costs
            for u, v, price in flights:
                if cost[u] + price < cur[v]:
                    cur[v] = cost[u] + price
            cost = cur
        return -1 if cost[dst] == INF else cost[dst]
```

## Time Complexity Analysis
> Time complexity  : O(k · E · log(k · E)) for Dijkstra; O(k · E) for Bellman-Ford (E = number of flights)
>
> Space complexity : O(k · E) for Dijkstra (heap); O(n) for Bellman-Ford

## Related Problems
- [743. Network Delay Time](https://leetcode.com/problems/network-delay-time) — 🟡 Medium · plain single-source Dijkstra
- [1514. Path with Maximum Probability](https://leetcode.com/problems/path-with-maximum-probability) — 🟡 Medium · Dijkstra with a different path metric
- [1631. Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort) — 🟡 Medium · Dijkstra on a grid with a modified cost
