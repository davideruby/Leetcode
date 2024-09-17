## [121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

<h2 style="color:#00b8a3">Easy</h2>

You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

## Solution
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        buyDay = 0
        max_profit = 0

        for sellDay in range(len(prices)):
            profit = prices[sellDay] - prices[buyDay]

            if profit < 0:
                buyDay = sellDay
            elif profit > max_profit:
                max_profit = profit

        return max_profit
```

## Notes
Initialize `buyDay = 0` and `sellDay = 1`. Determine `profit = prices[sellDay] - prices[buyDay]`. Check if the profit is the maximum found so far. Besides, if the `profit < 0`, it means we found a better day where buying stocks, so update `buyDay = sellDay`
