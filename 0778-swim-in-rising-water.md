## [778. Swim in Rising Water](https://leetcode.com/problems/swim-in-rising-water/description/)

${\textsf{\color{red}Hard}}$

You are given an n x n integer matrix grid where each value grid[i][j] represents the elevation at that point (i, j).

The rain starts to fall. At time t, the depth of the water everywhere is t. You can swim from a square to another 4-directionally adjacent square if and only if the elevation of both squares individually are at most t. You can swim infinite distances in zero time. Of course, you must stay within the boundaries of the grid during your swim.

Return the least time until you can reach the bottom right square (n - 1, n - 1) if you start at the top left square (0, 0).

## Solution
```python
import heapq

class Solution:
    def swimInWater(self, grid: List[List[int]]) -> int:
        costs = [ [float("inf")] * len(grid) for _ in range(len(grid))]
        costs[0][0] = grid[0][0]
        heap = [(costs[0][0], 0, 0)]
        
        while heap:
            cost, row, col = heapq.heappop(heap)

            for nr, nc in [ [1, 0], [-1, 0], [0, -1], [0, 1] ]:
                new_row = row + nr
                new_col = col + nc

                if 0 <= new_row < len(grid) and 0 <= new_col < len(grid):
                    neighbor_cost = max(cost, grid[new_row][new_col])

                    if neighbor_cost < costs[new_row][new_col]:
                        costs[new_row][new_col] = neighbor_cost
                        heapq.heappush(heap, (neighbor_cost, new_row, new_col))

        return costs[len(grid) - 1][len(grid) - 1]
```

## Notes
This problem is hard because it is more difficult to understand the description of the problem rather than understanding how to solve it. This solution uses the Dijkstra algorithm with a slight variation of the calculation of the cost.
