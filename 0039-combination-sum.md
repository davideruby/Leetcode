## [39. Combination Sum](https://leetcode.com/problems/combination-sum/)

<h2 style="color:#fac31d">Medium</h2>

Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order.

The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the 
frequency
 of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to target is less than 150 combinations for the given input.

## Solution
```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
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
            current.append(candidates[jdx])
            self.combinationSumHelper(candidates, target, combinations, current, jdx)
            current.pop()
```

## Notes
Basically, we have to generate all the possible combinations of the `candidates`. In order to repeat a candidate, in the for loop the first recursive call use the same index (instead of the next one, as in [77. Combinations](https://leetcode.com/problems/combinations/)).
