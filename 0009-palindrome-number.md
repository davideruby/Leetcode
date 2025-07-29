## [9. Palindrome Number](https://leetcode.com/problems/palindrome-number/description/)

${\textsf{\color{green}Easy}}$

Given an integer x, return true if x is a palindrome, and false otherwise.

## Solution
```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        forward = x
        backward = 0
        while x > 0:
            digit = x % 10
            x = x // 10

            backward = backward * 10 + digit

        return backward == forward
```
