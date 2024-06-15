## [40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)

<h2 style="color:#fac31d">Medium</h2>

Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target.

Each number in candidates may only be used once in the combination.

Note: The solution set must not contain duplicate combinations.

## Solution
```python
class Solution:
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort()
        combinations = []
        self.combinationSumHelper(candidates, target, combinations, [], 0)
        return combinations


    def combinationSumHelper(self, candidates: List[int], target: int, combinations: List[List[int]], current: List[int], idx: int) -> None:
        if sum(current) > target:
            return
        if sum(current) == target:
            combinations.append(current.copy())
            return

        for jdx in range(idx, len(candidates)):
            if jdx > idx and candidates[jdx] == candidates[jdx - 1]:
                continue

            current.append(candidates[jdx])
            self.combinationSumHelper(candidates, target, combinations, current, jdx + 1)
            current.pop()
```

## Notes
In addition to [39. Combination Sum](https://leetcode.com/problems/combination-sum/), you sort the `candidates` array and when you have not to include `candidates[jdx]` in the solution, you have not to include every candidate equal to `candidates[jdx]`.
