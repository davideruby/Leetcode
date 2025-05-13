## [853. Car Fleet](https://leetcode.com/problems/car-fleet/)

${\textsf{\color{yellow}Medium}}$

There are n cars at given miles away from the starting mile 0, traveling to reach the mile target.

You are given two integer array position and speed, both of length n, where position[i] is the starting mile of the ith car and speed[i] is the speed of the ith car in miles per hour.

A car cannot pass another car, but it can catch up and then travel next to it at the speed of the slower car.

A car fleet is a car or cars driving next to each other. The speed of the car fleet is the minimum speed of any car in the fleet.

If a car catches up to a car fleet at the mile target, it will still be considered as part of the car fleet.

Return the number of car fleets that will arrive at the destination.

## Solution
```python
class Solution:
    def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
        stack = []

        for pos, sp in sorted(zip(position, speed)):
            time = (target - pos) / sp
            while stack and time >= stack[-1]:
                stack.pop()

            stack.append(time)

        return len(stack)
```

## Notes
First, sort the position and speed array by position.
Then, use a monotonic stack: suppose you have two cars, the first starting with a greater position than the second one.
If the first car takes less step than the second car to get to the carget, it means we will have two car fleet.
Otherwise, if the first car takes more step than the second car, it means we will have just one car fleet.
