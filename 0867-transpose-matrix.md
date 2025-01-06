## [867. Transpose Matrix](https://leetcode.com/problems/transpose-matrix/)

${\textsf{\color{green}Easy}}$

Given a 2D integer array matrix, return the transpose of matrix.

The transpose of a matrix is the matrix flipped over its main diagonal, switching the matrix's row and column indices.

## Solution
```python
class Solution:
    def transpose(self, matrix: List[List[int]]) -> List[List[int]]:
        num_rows = len(matrix)
        num_cols = len(matrix[0])
        transpose = [ [0] * num_rows for _ in range(num_cols) ]

        for row in range(num_rows):
            for col in range(num_cols):
                transpose[col][row] = matrix[row][col]
        
        return transpose
```
