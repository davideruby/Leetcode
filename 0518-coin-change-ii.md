## [518. Coin Change II](https://leetcode.com/problems/coin-change-ii/)

${\textsf{\color{yellow}Medium}}$

You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.

Return the number of combinations that make up that amount. If that amount of money cannot be made up by any combination of the coins, return 0.

You may assume that you have an infinite number of each kind of coin.

The answer is guaranteed to fit into a signed 32-bit integer.

## Solution
```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        cache = [ [0] * (amount + 1) for _ in range(len(coins) + 1)]
        for idx in range(len(coins)):
            # with amount 0, we can have just one choice: don't take any coins.
            cache[idx][amount] = 1  

        for idx in range(len(coins) - 1, -1, -1):
            for jdx in range(amount - 1, -1, -1):
                cache[idx][jdx] = cache[idx + 1][jdx]
                if jdx + coins[idx] <= amount:
                    cache[idx][jdx] += cache[idx][jdx + coins[idx]]

        return cache[0][0]
```

## Notes
This is a dynamic programming problem.

The brute-force recursive solution is the following:
```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        return self.helper(amount, coins, 0)

    def helper(self, amount, coins, idx):
        if amount < 0:
            return 0
        if amount == 0:
            return 1
        if idx == len(coins):
            return 0

        return (
            self.helper(amount, coins, idx + 1) + 
            self.helper(amount - coins[idx], coins, idx)
        )
```

The idea is that when we deal with `coins[idx]`, we have two choices:
- either take the `coins[idx]` and call the recursive function with the remaining amount: `self.helper(amount - coins[idx], coins, idx)`, or:
- skip the `coins[idx]`, and recall the recursive function with the same amount: `self.helper(amount, coins, idx + 1)`.

I know that this might not be super intuitive but it is the most hard part.
Now, we can memoize this solution, to come up with this:
```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        return self.helper(amount, coins, 0, {})


    def helper(self, amount, coins, idx, cache):
        if amount < 0:
            return 0
        if amount == 0:
            return 1
        if idx == len(coins):
            return 0
        if (idx, amount) in cache:
            return cache[(idx, amount)]

        cache[(idx, amount)] = (
            self.helper(amount, coins, idx + 1, cache) + 
            self.helper(amount - coins[idx], coins, idx, cache)
        )

        return cache[(idx, amount)]
```

And then we can turn this solution into the iterative bottom-up version.