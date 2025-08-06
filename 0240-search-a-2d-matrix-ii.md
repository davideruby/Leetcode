## [240. Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/)

${\textsf{\color{yellow}Medium}}$

Write an efficient algorithm that searches for a value target in an m x n integer matrix matrix. This matrix has the following properties:

- Integers in each row are sorted in ascending from left to right.
- Integers in each column are sorted in ascending from top to bottom.

## Solution
```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        for row in matrix:
            if self.binarySearch(row, target):
                return True

        return False

    
    def binarySearch(self, nums, target):
        idx = 0
        jdx = len(nums) - 1

        while idx <= jdx:
            middle = (idx + jdx) // 2

            if nums[middle] < target:
                idx = middle + 1
            elif nums[middle] > target:
                jdx = middle - 1
            else:
                return True

        return False
```

## Notes
Easy binary search.
