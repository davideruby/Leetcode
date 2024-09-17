## [125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

<h2 style="color:#00b8a3">Easy</h2>

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

## Solution
```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        start = 0
        end = len(s) - 1

        while start < end:
            if not s[start].isalnum():
                start += 1
            elif not s[end].isalnum():
                end -= 1
            elif s[start].lower() == s[end].lower():
                start += 1
                end -= 1
            else:
                return False

        return True
```

