## [7. Reverse Integer](https://leetcode.com/problems/reverse-integer/)

${\textsf{\color{yellow}Medium}}$

Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-231, 231 - 1], then return 0.

Assume the environment does not allow you to store 64-bit integers (signed or unsigned).

## Solution
```python
class Solution:
    def reverse(self, x: int) -> int:
        num = abs(x)
        reverse = 0

        while num > 0:
            reverse = reverse * 10 + num % 10
            num = num // 10

        if reverse < -2**31 or reverse >= 2**31:
            return 0
        if x < 0:
            return -reverse
        return reverse
```

## Notes
At each iteration, take the last digit of the number with `num % 10` and add it to the reversed number, then divide the number by 10:
- num = 123, reverse = 0
- num = 12, reverse = 0 * 10 + 3 = 3
- num = 1, reverse = 3 * 10 + 2 = 32
- num = 0, reverse = 32 * 10 + 1 = 321
