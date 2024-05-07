## [74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)

<h2 style="color:#fac31d">Medium</h2>
You are given an m x n integer matrix matrix with the following two properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer target, return true if target is in matrix or false otherwise.

You must write a solution in O(log(m * n)) time complexity.

## Solution
```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        start = 0
        num_rows = len(matrix)
        num_cols = len(matrix[0])
        end = num_rows * num_cols - 1

        while start <= end:
            middle = (start + end) // 2
            middle_row = middle // num_cols
            middle_col = middle % num_cols
            middle_value = matrix[middle_row][middle_col]

            if middle_value < target:
                start = middle + 1
            elif middle_value > target:
                end = middle - 1
            else:
                return True
        
        return False
```

## Notes
Just a trick to convert the array index to matrix row and col.
