## [118. Pascal's Triangle](http://leetcode.com/problems/pascals-triangle/)

${\textsf{\color{green}Easy}}$

Given an integer numRows, return the first numRows of Pascal's triangle.

## Solution
```python
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        result = []
        prev = [1]

        for row in range(numRows):
            current = []
            for idx in range(row + 1):
                top_left = prev[idx - 1] if idx - 1 >= 0 else 0
                top_right = prev[idx] if idx < len(prev) else 0
                the_sum = top_left + top_right

                current.append(the_sum)

            result.append(current)
            prev = current

        return result
```
