## [48. Rotate Image](https://leetcode.com/problems/rotate-image/)

${\textsf{\color{yellow}Medium}}$

You are given an n x n 2D matrix representing an image, rotate the image by 90 degrees (clockwise).

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

## Solution
```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        num = len(matrix)
        left = 0
        right = num - 1

        while left < right:
            for idx in range(right - left):
                top = left
                bottom = right

                top_left = matrix[top][left + idx]
                matrix[top][left + idx] = matrix[bottom - idx][left]
                matrix[bottom - idx][left] = matrix[bottom][right - idx]
                matrix[bottom][right - idx] = matrix[top + idx][right]
                matrix[top + idx][right] = top_left

            left += 1
            right -= 1
        return
```

## Notes
Not a very straightforward problem. To be honest, I had to look at the solution, and I didn't learn so much. This problem is useful to practise with indices in a 2D array.

I also found another solution, which has a more simple code. It makes the transpose of the matrix and then reverse each row (simulate the solution to realize that it works):
```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        num = len(matrix)

        for row in range(num):
            for col in range(row, num):
                matrix[row][col], matrix[col][row] = matrix[col][row], matrix[row][col]

        for row in matrix:
            row.reverse()
```
