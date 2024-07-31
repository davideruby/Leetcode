## [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

<h2 style="color:#00b8a3">Easy</h2>
You are climbing a staircase. It takes n steps to reach the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

## Solution
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n <= 2:
            return n
            
        climb1 = 1
        climb2 = 2

        for idx in range(3, n + 1):
            tmp = climb1 + climb2
            climb1 = climb2
            climb2 = tmp

        return climb2
```

## Notes
If we are on the nth stair, either we climbed one stair from the (n - 1)th stair or we climbed two stairs from the (n - 2)th stair.
With this observation, we can apply the concept of Fibonacci series.