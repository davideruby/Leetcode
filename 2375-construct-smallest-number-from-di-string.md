## [2375. Construct Smallest Number From DI String](https://leetcode.com/problems/construct-smallest-number-from-di-string/)

${\textsf{\color{yellow}Medium}}$

You are given a 0-indexed string pattern of length n consisting of the characters 'I' meaning increasing and 'D' meaning decreasing.

A 0-indexed string num of length n + 1 is created using the following conditions:

- num consists of the digits '1' to '9', where each digit is used at most once.
- If pattern[i] == 'I', then num[i] < num[i + 1].
- If pattern[i] == 'D', then num[i] > num[i + 1].

Return the lexicographically smallest possible string num that meets the conditions.

## Solution
```python
class Solution:
    def smallestNumber(self, pattern: str) -> str:
        stack = []
        result = []

        for idx in range(len(pattern) + 1):
            stack.append(str(idx + 1))

            if idx == len(pattern) or pattern[idx] == "I":
                while stack:
                    result.append(stack.pop())

        return "".join(result)
```

## Notes
To be honest, I was not able to come up with a solution using the stack and having a linear time complexity. If you are not familiar with the stack, it is not so straightforward to understand this solution, so I encourage you to simulate the algorithm with pen and paper.
