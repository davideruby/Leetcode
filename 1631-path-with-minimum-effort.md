## [1631. Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort/)

${\textsf{\color{yellow}Medium}}$

You are a hiker preparing for an upcoming hike. You are given heights, a 2D array of size rows x columns, where heights[row][col] represents the height of cell (row, col). You are situated in the top-left cell, (0, 0), and you hope to travel to the bottom-right cell, (rows-1, columns-1) (i.e., 0-indexed). You can move up, down, left, or right, and you wish to find a route that requires the minimum effort.

A route's effort is the maximum absolute difference in heights between two consecutive cells of the route.

Return the minimum effort required to travel from the top-left cell to the bottom-right cell.

## Solution
```python
import heapq

class Solution:
    def minimumEffortPath(self, heights: List[List[int]]) -> int:
        num_rows, num_cols = len(heights), len(heights[0])
        heap = [(0, 0, 0)] # cost, row, column
        costs = [[float("inf")] * num_cols for _ in range(num_rows)]
        costs[0][0] = 0

        while heap:
            cost, row, col = heapq.heappop(heap)

            for nr, nc in [ [1, 0], [-1, 0], [0, 1], [0, -1] ]:
                neighbor_row = row + nr
                neighbor_col = col + nc

                if 0 <= neighbor_row < num_rows and 0 <= neighbor_col < num_cols:
                    neighbor_cost = max(
                        cost, 
                        abs(heights[neighbor_row][neighbor_col] - heights[row][col])
                    )

                    if neighbor_cost < costs[neighbor_row][neighbor_col]:
                        costs[neighbor_row][neighbor_col] = neighbor_cost
                        heapq.heappush(heap, (neighbor_cost, neighbor_row, neighbor_col))

        return costs[num_rows - 1][num_cols - 1]
```

## Notes
We can use Dijkstra, with a slight variation of the calculation of the cost: instead of aggregating the cost, we consider the absolute difference between two contiguos cells.
