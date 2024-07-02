## [994. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)

<h2 style="color:#fac31d">Medium</h2>
You are given an m x n grid where each cell can have one of three values:

- 0 representing an empty cell,
- 1 representing a fresh orange, or
- 2 representing a rotten orange.

Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten.

Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return -1.

## Solution
```python
from collections import deque

class Solution:
    def orangesRotting(self, grid: List[List[int]]) -> int:
        FRESH = 1
        ROTTEN = 2
        queue = deque()
        fresh_count = 0
        num_rows = len(grid)
        num_cols = len(grid[0])

        for row in range(num_rows):
            for col in range(num_cols):
                if grid[row][col] == FRESH:
                    fresh_count += 1
                elif grid[row][col] == ROTTEN:
                    queue.append((row, col))

        visited = set()
        minutes = 0
        while queue and fresh_count > 0:
            for _ in range(len(queue)):
                row, col = queue.popleft()

                for nr, nc in [ [-1, 0], [1, 0], [0, -1], [0, 1] ]:
                    new_row = row + nr
                    new_col = col + nc

                    if (0 <= new_row < num_rows and
                        0 <= new_col < num_cols and
                        grid[new_row][new_col] == FRESH and
                        (new_row, new_col) not in visited):
                        queue.append((new_row, new_col))
                        visited.add((new_row, new_col))
                        fresh_count -= 1
            minutes += 1
        
        return minutes if fresh_count == 0 else -1
```

## Notes
Perform a breadth first search on the grid, starting from every rotten orange.
