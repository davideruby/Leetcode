## [1267. Count Servers that Communicate](https://leetcode.com/problems/count-servers-that-communicate/)

${\textsf{\color{yellow}Medium}}$

You are given a map of a server center, represented as a m * n integer matrix grid, where 1 means that on that cell there is a server and 0 means that it is no server. Two servers are said to communicate if they are on the same row or on the same column.

Return the number of servers that communicate with any other server.

## Solution
```python
class Solution:
    def countServers(self, grid: List[List[int]]) -> int:
        num_rows = len(grid)
        num_cols = len(grid[0])
        SERVER = 1

        server_rows = [0] * num_rows
        server_cols = [0] * num_cols
        for row in range(num_rows):
            for col in range(num_cols):
                if grid[row][col] == SERVER:
                    server_rows[row] += 1
                    server_cols[col] += 1

        isolated = 0
        total = 0
        for row in range(num_rows):
            for col in range(num_cols):
                if grid[row][col] == SERVER:
                    total += 1
                    if server_rows[row] == 1 and server_cols[col] == 1:
                        isolated += 1
        
        return total - isolated
```

## Notes
No DFS or BFS on a graph, but count how many servers are isolated. 
Count how many servers there are for each row and column. Then, a server is isolated if it is alone along its row and its column.
