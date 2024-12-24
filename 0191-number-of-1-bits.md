## [191. Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)

${\textsf{\color{green}Easy}}$

Given a positive integer n, write a function that returns the number of set bits in its binary representation (also known as the Hamming weight).

## Solution
```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        hamming_weight = 0

        while n > 0:
            hamming_weight += n % 2
            n = n // 2

            # If you want a super optimized version:
            # hamming_weight += 1
            # n &= (n - 1)
        
        return hamming_weight
```
