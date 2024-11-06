## [66. Plus One](https://leetcode.com/problems/plus-one/)

${\textsf{\color{green}Easy}}$

Problem description

## Solution
```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        carry = 1

        for idx in range(len(digits) - 1, -1, -1):
            plus_one = digits[idx] + carry
            new_digit = plus_one % 10
            carry = plus_one // 10
            digits[idx] = new_digit

        return digits if carry == 0 else [1] + digits
```

## Notes
Think how we used to do additions in elementary school.
