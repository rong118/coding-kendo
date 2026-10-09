# 121. Best Time to Buy and Sell Stock

**Difficulty:** 🟢 Easy

## Question link
(https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

## Question Description
You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

Example 1:

> Input: prices = [7,1,5,3,6,4]
>
> Output: 5
> 
> Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
>
> Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

Example 2:

> Input: prices = [7,6,4,3,1]
>
> Output: 0
>
> Explanation: In this case, no transactions are done and the max profit = 0.
 

Constraints:

1 <= prices.length <= 10^5
0 <= prices[i] <= 10^4

## Tags
- Array
- Dynamic Programming

## Approach
**Key idea:** The best sale on day `i` buys at the lowest price seen before it, so one pass tracking the running minimum is enough.

1. Set `low` to the first price and `best = 0`.
2. For each price, if it is lower than `low`, it becomes the new buying price.
3. Otherwise, selling today earns `price - low`; update `best` with it.
4. Return `best` (0 if prices only fall).

## Code Implementation
```python
class Solution:
    def maxProfit(self, prices: list[int]) -> int:
        low = prices[0]
        best = 0
        for price in prices:
            if price < low:
                low = price
            else:
                best = max(best, price - low)
        return best
```

## Time Complexity Analysis
> Time complexity  : O(n)
>
> Space complexity : O(1)

## Related Problems
- [122. Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii) — 🟡 Medium · unlimited transactions, greedy
- [123. Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii) — 🔴 Hard · at most two transactions, DP
- [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray) — 🟡 Medium · one-pass running best (Kadane's algorithm)
