## [2661. First Completely Painted Row or Column](https://leetcode.com/problems/first-completely-painted-row-or-column/)

${\textsf{\color{yellow}Medium}}$

You are given a 0-indexed integer array arr, and an m x n integer matrix mat. arr and mat both contain all the integers in the range [1, m * n].

Go through each index i in arr starting from index 0 and paint the cell in mat containing the integer arr[i].

Return the smallest index i at which either a row or a column will be completely painted in mat.

## Solution
```python
class Solution:
    def firstCompleteIndex(self, arr: List[int], mat: List[List[int]]) -> int:
        num_rows = len(mat)
        num_cols = len(mat[0])

        num_to_indices = {}
        for row in range(num_rows):
            for col in range(num_cols):
                num = mat[row][col]
                num_to_indices[num] = (row, col)

        
        uncolored_rows = [num_cols] * num_rows
        uncolored_cols = [num_rows] * num_cols
        for idx, num in enumerate(arr):
            row, col = num_to_indices[num]
            uncolored_rows[row] -= 1
            uncolored_cols[col] -= 1
            
            if uncolored_rows[row] == 0 or uncolored_cols[col] == 0:
                return idx
        
        raise "should not fall here :("
```

## Notes
For a given number, how can I access to its position in the matrix in O(1)? Use a hashmap that maps each number to its row and column in `mat`.
How can I know if a row or a column is fully colored in O(1)? Use two arrays to track the remaining uncolored cells for each row and column.
