## [1415. The k-th Lexicographical String of All Happy Strings of Length n](https://leetcode.com/problems/the-k-th-lexicographical-string-of-all-happy-strings-of-length-n/)

${\textsf{\color{yellow}Medium}}$

A happy string is a string that:

- consists only of letters of the set ['a', 'b', 'c'].
- s[i] != s[i + 1] for all values of i from 1 to s.length - 1 (string is 1-indexed).

For example, strings "abc", "ac", "b" and "abcbabcbcb" are all happy strings and strings "aa", "baa" and "ababbc" are not happy strings.

Given two integers n and k, consider a list of all happy strings of length n sorted in lexicographical order.

Return the kth string of this list or return an empty string if there are less than k happy strings of length n.

## Solution
```python
class Solution:
    def getHappyString(self, n: int, k: int) -> str:
        happy_string = []
        self.backtracking(n, k, happy_string, [0])
        return "".join(happy_string)


    def backtracking(self, n: int, k: int, current: List[str], idx: List[int]):
        if len(current) == n:
            idx[0] += 1
            return idx[0] == k

        for char in "abc":
            if len(current) > 0 and char == current[-1]:
                continue
                
            current.append(char)
            if self.backtracking(n, k, current, idx):
                return True
            current.pop()

        return False
```

## Notes
A solution using backtracking. Basically it computes every single happy string and then return the k-th. I used the trick to put the index in an array of a single element to keep track of the number of solutions found so far.
