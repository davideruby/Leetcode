## [3355. Zero Array Transformation I](https://leetcode.com/problems/zero-array-transformation-i/)

${\textsf{\color{yellow}Medium}}$

Problem description

## Solution
```python
class Solution:
    def isZeroArray(self, nums: List[int], queries: List[List[int]]) -> bool:
        line = [0] * (len(nums) + 1)

        for left, right in queries:
            line[left] += 1
            line[right + 1] -= 1

        for idx in range(1, len(line)):
            line[idx] += line[idx - 1]

        for idx in range(len(nums)):
            if line[idx] < nums[idx]:
                return False

        return True
```

## Notes
Use difference array and prefix sum to check if an index can be made zero. 

For any `queries[i] = [l, r]`, increment `line[l]` and decrement `line[r + 1]`: that means a query decrements every element in the interval `[l, r]`.
Then, use prefix sum to compute if all elements can be made zero.