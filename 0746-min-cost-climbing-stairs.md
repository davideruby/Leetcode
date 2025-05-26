## [746. Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/)

${\textsf{\color{green}Easy}}$

You are given an integer array cost where cost[i] is the cost of ith step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from the step with index 0, or the step with index 1.

Return the minimum cost to reach the top of the floor.

## Solution
```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        min_cost = 0
        min1 = cost[0]
        min2 = cost[1]

        for idx in range(2, len(cost)):
            min_cost = cost[idx] + min(min1, min2)
            min1 = min2
            min2 = min_cost

        return min(min1, min2)
```

## Notes
Very similar to the Fibonacci problem.
