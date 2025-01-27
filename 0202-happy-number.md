## [202. Happy Number](https://leetcode.com/problems/happy-number/description/)

${\textsf{\color{green}Easy}}$

Write an algorithm to determine if a number n is happy.

A happy number is a number defined by the following process:

- Starting with any positive integer, replace the number by the sum of the squares of its digits.
- Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
- Those numbers for which this process ends in 1 are happy.

Return true if n is a happy number, and false if not.

## Solution
```python
class Solution:
    def isHappy(self, n: int) -> bool:
        previous = set()
        num = n

        while num not in previous and num != 1:
            previous.add(num)
            num = self.getNext(num)

        return num == 1

    def getNext(self, num: int) -> int:
        next_num = 0
        
        while num > 0:
            digit = num % 10
            next_num += digit ** 2
            num = num // 10

        return next_num
```
