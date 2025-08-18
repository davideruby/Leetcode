## [2264. Largest 3-Same-Digit Number in String](https://leetcode.com/problems/largest-3-same-digit-number-in-string/)

${\textsf{\color{green}Easy}}$

You are given a string num representing a large integer. An integer is good if it meets the following conditions:

- It is a substring of num with length 3.
- It consists of only one unique digit.

Return the maximum good integer as a string or an empty string "" if no such integer exists.

Note:

- A substring is a contiguous sequence of characters within a string.
- There may be leading zeroes in num or a good integer.

## Solution
```python
class Solution:
    def largestGoodInteger(self, num: str) -> str:
        largest = -1

        for idx in range(2, len(num)):
            if num[idx - 2] == num[idx - 1] == num[idx]:
                largest = max(largest, int(num[idx - 2: idx + 1]))

        return f"{largest:03d}" if largest != -1 else ""
```
