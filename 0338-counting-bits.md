## [338. Counting Bits](https://leetcode.com/problems/counting-bits/)

${\textsf{\color{green}Easy}}$

Given an integer n, return an array ans of length n + 1 such that for each i (0 <= i <= n), ans[i] is the number of 1's in the binary representation of i.

## Solution
```python
class Solution:
    def countBits(self, n: int) -> List[int]:
        counts = [0]
        offset = 1

        for num in range(1, n + 1):
            if num == 2 * offset:
                offset *= 2
            
            counts.append(1 + counts[num - offset])

        return counts
```

## Notes
This is a solution using dynamic programming to achieve O(n) time complexity.
The idea is the following:
- 0 (0000) has 0 ones
- 1 (0001) has 1 ones
- 2 (0010) has 1 one + the number of ones contained in 0 (2 - 2)
- 3 (0011) has 1 one + the number of ones contained in 1 (3 - 2)
- 4 (0100) has 1 one + the number of ones contained in 0 (4 - 4)
- 5 (0101) has 1 one + the number of ones contained in 1 (5 - 4)
- 6 (0110) has 1 one + the number of ones contained in 2 (6 - 4)
- 7 (0111) has 1 one + the number of ones contained in 3 (7 - 4)
- 8 (1000) has 1 one + the number of ones contained in 0 (8 - 8)
- ....
