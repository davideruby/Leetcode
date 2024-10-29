## [62. Unique Paths](https://leetcode.com/problems/unique-paths/)

${\textsf{\color{yellow}Medium}}$

There is a robot on an m x n grid. The robot is initially located at the top-left corner (i.e., grid[0][0]). The robot tries to move to the bottom-right corner (i.e., grid[m - 1][n - 1]). The robot can only move either down or right at any point in time.

Given the two integers m and n, return the number of possible unique paths that the robot can take to reach the bottom-right corner.

The test cases are generated so that the answer will be less than or equal to 2 * 10^9.

## Solution
```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        prev_row = [0] * n

        for row in range(m - 1, -1, -1):
            cur_row = [0] * n
            cur_row[-1] = 1

            for col in range(n - 2, -1, -1):
                cur_row[col] = prev_row[col] + cur_row[col + 1]

            prev_row = cur_row

        return cur_row[0]
```

## Notes
This is a dynamic programming problem.

First of all, let's check the bruteforce solution:
```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        return self.bruteforce(m, n, 0, 0)

    def bruteforce(self, num_rows: int, num_cols: int, row: int, col: int):
        if row >= num_rows or col >= num_cols:
            return 0
        if row == num_rows - 1 and col == num_cols - 1:
            return 1
        
        return (self.bruteforce(num_rows, num_cols, row + 1, col) + 
                self.bruteforce(num_rows, num_cols, row, col + 1))
```

Then, let's use a `cache` not to do repeated work:
```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        cache = [[0] * n for _ in range(m)]
        return self.memo(m, n, 0, 0, cache)

    def memo(self, num_rows: int, num_cols: int, row: int, col: int, cache: list[list[int]]):
        if row >= num_rows or col >= num_cols:
            return 0
        if row == num_rows - 1 and col == num_cols - 1:
            return 1
        if cache[row][col] == 0:
            cache[row][col] = (self.memo(num_rows, num_cols, row + 1, col, cache) + 
                               self.memo(num_rows, num_cols, row, col + 1, cache))
        return cache[row][col]
```

Pretty simple, isn't it? Now, we have to get rid of the `cache` of size `n * m`. To do so, we have to turn this top-down solution into the bottom-up one. The idea is that we start from the most bottom-right cell. Then, for each cell, we can notice that we need just the value of the cell below (`prev_row[col]`) of the cell to the right (`cur_row[col + 1]`). 