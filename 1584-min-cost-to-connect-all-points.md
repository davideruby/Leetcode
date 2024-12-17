## [1584. Min Cost to Connect All Points](https://leetcode.com/problems/min-cost-to-connect-all-points/)

${\textsf{\color{yellow}Medium}}$

You are given an array points representing integer coordinates of some points on a 2D-plane, where points[i] = [xi, yi].

The cost of connecting two points [xi, yi] and [xj, yj] is the manhattan distance between them: |xi - xj| + |yi - yj|, where |val| denotes the absolute value of val.

Return the minimum cost to make all points connected. All points are connected if there is exactly one simple path between any two points.

## Solution
```python
import heapq

class Solution:
    def minCostConnectPoints(self, points: List[List[int]]) -> int:
        heap = [(0, 0)]
        mst = { 0: 0 }
        visited = set()

        while heap:
            weight, node = heapq.heappop(heap)
            if node in visited:
                continue

            visited.add(node)
            mst[node] = weight

            for neighbor in range(len(points)):
                if neighbor not in visited:
                    distance = self.manhattanDistance(points[node], points[neighbor])
                    heapq.heappush(heap, (distance, neighbor))
        
        return sum(mst.values())

    
    def manhattanDistance(self, pointA, pointB):
        return abs(pointA[0] - pointB[0]) + abs(pointA[1] - pointB[1])
```

## Notes
Prim's algorithm.
