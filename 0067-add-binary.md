## [67. Add Binary](https://leetcode.com/problems/add-binary/)

${\textsf{\color{green}Easy}}$

Given two binary strings a and b, return their sum as a binary string.

## Solution
```python
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        idx_a = len(a) - 1
        idx_b = len(b) - 1
        str_sum = ""
        carry = 0

        while idx_a >= 0 or idx_b >= 0:
            first = int(a[idx_a]) if idx_a >= 0 else 0
            second = int(b[idx_b]) if idx_b >= 0 else 0

            the_sum = first + second + carry
            next_digit = the_sum % 2
            str_sum = str(next_digit) + str_sum

            carry = the_sum // 2
            idx_a -= 1
            idx_b -= 1

        if carry > 0:
            str_sum = str(carry) + str_sum

        return str_sum
```
