## [77. Combinations](https://leetcode.com/problems/combinations/)

<h2 style="color:#fac31d">Medium</h2>

Given two integers n and k, return all possible combinations of k numbers chosen from the range [1, n].

You may return the answer in any order.

## Solution
```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        combinations = []
        self.combineHelper(n, k, combinations, [], 1)
        return combinations
        

    def combineHelper(self, n: int, k: int, combinations: List[List[int]], current: List[int], num: int) -> None:
        if len(current) == k:
            combinations.append(current.copy())
            return
        
        for next_num in range(num, n + 1):
            current.append(next_num)
            self.combineHelper(n, k, combinations, current, next_num + 1)
            current.pop()
```

