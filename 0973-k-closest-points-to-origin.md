## [973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)

<h2 style="color:#fac31d">Medium</h2>

Given an array of points where points[i] = [xi, yi] represents a point on the X-Y plane and an integer k, return the k closest points to the origin (0, 0).

The distance between two points on the X-Y plane is the Euclidean distance (i.e., √(x1 - x2)2 + (y1 - y2)2).

You may return the answer in any order. The answer is guaranteed to be unique (except for the order that it is in).


## Solution
```python
import heapq

class Solution:
    def kClosest(self, points: List[List[int]], k: int) -> List[List[int]]:
        heap = []

        for point in points:
            distance = (point[0] ** 2) + (point[1] **2)
            distance = -distance

            if len(heap) < k:
                heapq.heappush(heap, (distance, point))
            elif distance > heap[0][0]:
                heapq.heappop(heap)
                heapq.heappush(heap, (distance, point))
                
        return [point for dist, point in heap]
```

## Notes
Use a max-heap that stores the k closest points. If you don't know how to implement a max-heap in python, use the standard library `heapq` and insert every value multiplied by `-1`.