## [1323. Maximum 69 Number](https://leetcode.com/problems/maximum-69-number/)

${\textsf{\color{green}Easy}}$

You are given a positive integer num consisting only of digits 6 and 9.

Return the maximum number you can get by changing at most one digit (6 becomes 9, and 9 becomes 6).

## Solution
```python
class Solution:
    def maximum69Number (self, num: int) -> int:
        chars_num = list(str(num))

        for idx, char in enumerate(chars_num):
            if char == "6":
                chars_num[idx] = "9"
                break

        return int("".join(chars_num))
```
