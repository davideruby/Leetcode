## [739. Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)

<h2 style="color:#fac31d">Medium</h2>
Given an array of integers temperatures represents the daily temperatures, return an array answer such that answer[i] is the number of days you have to wait after the ith day to get a warmer temperature. If there is no future day for which this is possible, keep answer[i] == 0 instead.

## Solution
```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        stack = []
        answer = [0] * len(temperatures)

        for idx, temp in enumerate(temperatures):
            while len(stack) > 0 and temp > stack[-1][0]:
                [lower_temp, idx_lower_temp] = stack.pop()
                answer[idx_lower_temp] = idx - idx_lower_temp

            stack.append([temp, idx])
        return answer

    # version 2
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        stack = []
        result = [0] * len(temperatures)

        for idx, temp in enumerate(temperatures):
            while len(stack) > 0 and temp > temperatures[stack[-1]]:
                lower_temperature_idx = stack.pop()
                result[lower_temperature_idx] = idx - lower_temperature_idx

            stack.append(idx)
        return result
```

## Notes
- Use a monotonic stack: push the temperature and the index where the temperature is. Before pushing it, pop the stack as long as the current temperature is greater than the top of the stack: it means that the current temperature is the next greater tempearture. Save in the answer the difference between the index of the current temperature and the popped temperature.
- Version 2 consists of pushing in the stack only the indexes of the temperatures (the temperature can be gotten by `temperatures[stack[-1]]`)
