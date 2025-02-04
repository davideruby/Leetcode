## [2013. Detect Squares](https://leetcode.com/problems/detect-squares/)

${\textsf{\color{yellow}Medium}}$

You are given a stream of points on the X-Y plane. Design an algorithm that:

- Adds new points from the stream into a data structure. Duplicate points are allowed and should be treated as different points.
- Given a query point, counts the number of ways to choose three points from the data structure such that the three points and the query point form an axis-aligned square with positive area.

An axis-aligned square is a square whose edges are all the same length and are either parallel or perpendicular to the x-axis and y-axis.

Implement the DetectSquares class:

- DetectSquares() Initializes the object with an empty data structure.
- void add(int[] point) Adds a new point point = [x, y] to the data structure.
- int count(int[] point) Counts the number of ways to form axis-aligned squares with point point = [x, y] as described above.

## Solution
```python
class DetectSquares:

    def __init__(self):
        self.points = {}

    def add(self, point: List[int]) -> None:
        x, y = point
        if x not in self.points:
            self.points[x] = {}
        if y not in self.points[x]:
            self.points[x][y] = 0
        self.points[x][y] += 1

    def count(self, point: List[int]) -> int:
        px, py = point
        count = 0

        for x in self.points.keys():
            for y in self.points[x].keys():
                if x != px and abs(y - py) == abs(x - px):
                    count += self.points[x][y] * self.points[x].get(py, 0) * self.points.get(px, {}).get(y, 0)
        
        return count
```

## Notes
I used two nested hashmaps to keep track of how many points there are on each coordinate.
Then, the brute force solution takes `O(n^3)` time, but there is a trick.
Suppose the count function receives in input the point `(px, py)`. Then, we have to find every point `(x, y)` such that `(x, y)` and `(px, py)` are the two point on a diagonal of the square, that said `Δy / Δx = 1 -> Δy = Δx -> abs(py - y) == abs(px - x)`.
    (px,py)
     /
    /
   /
(x, y)


Then, the other two points of the square are `(x, py)` and `(px, y)`.
(x, py)--------(px,py)
   |               | 
   |               |
   |               | 
(x, y)---------(px, y)

In this way, we can build a `O(n^2)` solution.