## [3223. Minimum Length of String After Operations](https://leetcode.com/problems/minimum-length-of-string-after-operations/)

${\textsf{\color{yellow}Medium}}$

You are given a string s.

You can perform the following process on s any number of times:

- Choose an index i in the string such that there is at least one character to the left of index i that is equal to s[i], and at least one character to the right that is also equal to s[i].
- Delete the closest character to the left of index i that is equal to s[i].
- Delete the closest character to the right of index i that is equal to s[i].

Return the minimum length of the final string s that you can achieve.

## Solution
```python
class Solution:
    def minimumLength(self, s: str) -> int:
        counts = Counter(s)

        final_length = 0
        for count in counts.values():
            if count % 2 == 0:
                final_length += 2
            else:
                final_length += 1
        
        return final_length
```

## Notes
Initally, I solved the problem counting how many characters there are on the left and on the right of each character, but then I realized the only thing that matters is the frequency of each character.

For example, if a characters appears 3 times, only one will remain; if a characters appears 4 times, only two will remain, and so on.