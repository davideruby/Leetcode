## [875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)

<h2 style="color:#fac31d">Medium</h2>
Koko loves to eat bananas. There are n piles of bananas, the ith pile has piles[i] bananas. The guards have gone and will come back in h hours.

Koko can decide her bananas-per-hour eating speed of k. Each hour, she chooses some pile of bananas and eats k bananas from that pile. If the pile has less than k bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return the minimum integer k such that she can eat all the bananas within h hours.

## Solution
```python
import math

class Solution:
    def minEatingSpeed(self, piles: List[int], h: int) -> int:
        min_speed = 1
        max_speed = max(piles)

        while min_speed <= max_speed:
            middle_speed = (min_speed + max_speed) // 2
            hours = self.getHoursToEat(piles, middle_speed)

            if hours > h:
                min_speed = middle_speed + 1
            else:
                max_speed = middle_speed - 1
        
        return min_speed

    def getHoursToEat(self, piles, speed):
        hours = 0
        for pile in piles:
            hours += math.ceil(pile / speed)
        return hours
```

## Notes
The minimum speed is 1 banana per hour, the maximum speed is `max(piles)` (and so `k > piles.length`).
Find the target speed with a binary search.

