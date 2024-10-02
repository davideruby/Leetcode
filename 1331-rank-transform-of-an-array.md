## [1331. Rank Transform of an Array](https://leetcode.com/problems/rank-transform-of-an-array/)

<h2 style="color:#00b8a3">Easy</h2>

Given an array of integers arr, replace each element with its rank.

The rank represents how large the element is. The rank has the following rules:

- Rank is an integer starting from 1.
- The larger the element, the larger the rank. If two elements are equal, their rank must be the same.
- Rank should be as small as possible.

## Solution
```python
class Solution:
    def arrayRankTransform(self, arr: List[int]) -> List[int]:
        sorted_arr = sorted(arr)
        ranks = {}
        rank = 1

        for idx, num in enumerate(sorted_arr):
            ranks[num] = rank

            if idx < len(sorted_arr) - 1 and num < sorted_arr[idx + 1]:
                rank += 1
        
        return [ranks[num] for num in arr]
```

## Notes
Get a sorted copy of the original array. Then, use the sorted array to store in a hashmap the rank of each number.
