## [3160. Find the Number of Distinct Colors Among the Balls](https://leetcode.com/problems/find-the-number-of-distinct-colors-among-the-balls/)

${\textsf{\color{yellow}Medium}}$

You are given an integer limit and a 2D array queries of size n x 2.

There are limit + 1 balls with distinct labels in the range [0, limit]. Initially, all balls are uncolored. For every query in queries that is of the form [x, y], you mark ball x with the color y. After each query, you need to find the number of distinct colors among the balls.

Return an array result of length n, where result[i] denotes the number of distinct colors after ith query.

Note that when answering a query, lack of a color will not be considered as a color.

## Solution
```python
class Solution:
    def queryResults(self, limit: int, queries: List[List[int]]) -> List[int]:
        result = []
        count = 0
        colors_count = {}
        balls = {}

        for ball, color in queries:
            if ball in balls:
                old_color = balls[ball]
                colors_count[old_color] -= 1

                if colors_count[old_color] == 0:
                    count -= 1
            
            balls[ball] = color
            colors_count[color] = colors_count.get(color, 0) + 1
            if colors_count[color] == 1:
                count += 1

            result.append(count)

        return result
```

## Notes
The trivial solution is to use a hashmap to keep track of the color of each ball, and each time count how many colors are used. This solution has O(n^2) time complexity.

The trick to get a solution with O(n) time complexity is to use an additional hashmap which keeps track for each color how many times it is used.
