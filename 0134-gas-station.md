## [134. Gas Station](https://leetcode.com/problems/gas-station/description/)

<h2 style="color:#fac31d">Medium</h2>

There are n gas stations along a circular route, where the amount of gas at the ith station is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from the ith station to its next (i + 1)th station. You begin the journey with an empty tank at one of the gas stations.

Given two integer arrays gas and cost, return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1. If there exists a solution, it is guaranteed to be unique.

## Solution
```python
class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:
        if sum(gas) < sum(cost): 
            return -1

        fuel = 0
        start = 0

        for idx in range(len(gas)):
            if fuel < 0:
                start = idx
                fuel = 0

            fuel += gas[idx] - cost[idx]
            
        return start
```

## Notes
The code is very simple, but understanding the solution is very hard.
This solution has `O(n)` time complexity, because it iterates the array just once.

The idea is:
- If `sum(gas) < sum(cost)`, then return `-1`.
- We start from position `idx` (initially `idx = 0`)
- At each step we update our current fuel, with `fuel += gas[idx] - cost[idx]`.
- If the remaining fuel is `< 0`, it means we cannot start from any previous position. 
    - Why is that? Well, let's suppose we started from `A`, we arrived to `C` with `fuel < 0` and there is a position `B` between `A` and `C` with `fuel > 0`: `A ---> B(fuel > 0) ---> C(fuel < 0)`. Starting from `B` makes no sense at all: we started from `A`, arrived to `B` with `fuel > 0` and didn't arrive to `C`, how the hell could we arrive to `C` starting from `B` with `fuel = 0`?!
    - So, if `fuel < 0`, restart our search from the current index.
- If the current fuel is `> 0`, we have to do nothing, we just keep track of the index from which we started previously. 
    - Why is that? Well, this is similar to previous explanation. 
    If we have `A (fuel > 0) ----> B (fuel > 0) ----> C` and we are in `A`, it makes no sense to start from `B`, because we are more likely to travel around the circuit starting from `A` and getting to `B` with `fuel > 0` rather then starting from `B` with `fuel = 0`.