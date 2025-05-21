## [73. Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/description/)

${\textsf{\color{yellow}Medium}}$

Given an m x n integer matrix matrix, if an element is 0, set its entire row and column to 0's.

You must do it in place.

## Solution
```python
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        rows_zero = []
        cols_zero = []

        for row in range(len(matrix)):
            for col in range(len(matrix[row])):
                if matrix[row][col] == 0:
                    rows_zero.append(row)
                    cols_zero.append(col)

        for row in rows_zero:
            for col in range(len(matrix[row])):
                matrix[row][col] = 0

        for col in cols_zero:
            for row in range(len(matrix)):
                matrix[row][col] = 0
```

