## [322. Coin Change](https://leetcode.com/problems/coin-change/)

<h2 style="color:#fac31d">Medium</h2>

You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

You may assume that you have an infinite number of each kind of coin.

## Solution
```python
# O(n * amount) time, O(n) space.
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [0] * (amount + 1)
        dp[0] = 0

        for am in range(1, amount + 1):
            dp[am] = float("inf")

            for coin in coins:
                if am - coin >= 0:
                    dp[am] = min(dp[am], 1 + dp[am - coin])
        
        return dp[amount] if dp[amount] != float("inf") else -1
```

## Notes
The first time, I solved this problem through a backtracking algorithm, but then I realized there was a better solution with dynamic programming.

Here the comment I found on Leetcode that helped me the most:

Take `coins=[1, 2, 5]` and `amount = 11` as an example,

- If I use one `1`, I need to know the fewest number of coins I need to make up `10`, i.e., `dp[10]`. Overall I need `1 + dp[10]` coins.
- If I use one `2`, I need `1 + dp[9]` coins.
- If I use one `5`, I need `1 + dp[6]` coins.

Therefore, I need to calculate `dp` from `1` to `amount`.
