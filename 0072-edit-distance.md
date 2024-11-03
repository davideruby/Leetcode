## [72. Edit Distance](https://leetcode.com/problems/edit-distance/)

${\textsf{\color{yellow}Medium}}$

Given two strings word1 and word2, return the minimum number of operations required to convert word1 to word2.

You have the following three operations permitted on a word:

- Insert a character
- Delete a character
- Replace a character

## Solution
```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        prev_row = [len(word2) - idx2 for idx2 in range(len(word2) + 1)]

        for idx1 in range(len(word1) - 1, -1, -1):
            cur_row = [0] * (len(word2) + 1)
            cur_row[-1] = len(word1) - idx1

            for idx2 in range(len(word2) - 1, -1, -1):
                if word1[idx1] == word2[idx2]:
                    cur_row[idx2] = prev_row[idx2 + 1]
                else:
                    insert = 1 + cur_row[idx2 + 1]
                    delete = 1 + prev_row[idx2]
                    replace = 1 + prev_row[idx2 + 1]
                    cur_row[idx2] = min(insert, delete, replace)

            prev_row = cur_row
                    
        return prev_row[0]
```

## Notes
This is a dynamic programming problem. To come up with this solution, the first thing is to understand the recursive brute-force solution:
- if one of the two strings is empty, the edit distance is the length of the other string.
- if the characters at the current positions are equal, we have to increment both of the indexes.
- otherwise, we have to take into account the 3 possible operations:
    - Insert: if we insert a character in `word1`, we have satisfied the current character of `word2`, so we have to increment the index2.
    - Delete: if we delete the current character of `word1`, we have to check the next character of `word1`, so we have to increment the index1.
    - Replace: we replace the current character of `word1` with the current character of `word2`, so the current characters of both strings now match and we have to go to the next characters of both strings (increment both indexes).

```python
# O(3^(n + m)) time, O(1) space
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        return self.helper(word1, word2, 0, 0)

    def helper(self, word1: str, word2: str, idx1: int, idx2: int):
        if idx1 == len(word1):
            return len(word2) - idx2
        if idx2 == len(word2):
            return len(word1) - idx1

        if word1[idx1] == word2[idx2]:
            return self.helper(word1, word2, idx1 + 1, idx2 + 1)
        
        insert = 1 + self.helper(word1, word2, idx1, idx2 + 1)
        delete = 1 + self.helper(word1, word2, idx1 + 1, idx2)
        replace = 1 + self.helper(word1, word2, idx1 + 1, idx2 + 1)
        return min(insert, delete, replace)
```

Then, the recursive memoized version is pretty simple:
```python
# O(n*m) time, O(n*m) space
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        cache = [ [-1] * len(word2) for _ in range(len(word1))]
        return self.helper(word1, word2, 0, 0, cache)

    def helper(self, word1: str, word2: str, idx1: int, idx2: int, cache: List[List[int]]):
        if idx1 == len(word1):
            return len(word2) - idx2
        if idx2 == len(word2):
            return len(word1) - idx1

        if cache[idx1][idx2] != -1:
            return cache[idx1][idx2]

        if word1[idx1] == word2[idx2]:
            cache[idx1][idx2] = self.helper(word1, word2, idx1 + 1, idx2 + 1, cache)
        else:
            insert = 1 + self.helper(word1, word2, idx1, idx2 + 1, cache)
            delete = 1 + self.helper(word1, word2, idx1 + 1, idx2, cache)
            replace = 1 + self.helper(word1, word2, idx1 + 1, idx2 + 1, cache)
            cache[idx1][idx2] = min(insert, delete, replace)
            
        return cache[idx1][idx2]
```

Now, let's turn this solution into the iterative bottom-up one:
```python
# O(n*m) time, O(n*m) space
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        cache = [ [0] * (len(word2) + 1) for _ in range(len(word1) + 1)]

        for idx1 in range(len(word1)):
            cache[idx1][-1] = len(word1) - idx1

        for idx2 in range(len(word2)):
            cache[-1][idx2] = len(word2) - idx2
        
        for idx1 in range(len(word1) - 1, -1, -1):
            for idx2 in range(len(word2) - 1, -1, -1):
                if word1[idx1] == word2[idx2]:
                    cache[idx1][idx2] = cache[idx1 + 1][idx2 + 1]
                else:
                    insert = 1 + cache[idx1][idx2 + 1]
                    delete = 1 + cache[idx1 + 1][idx2]
                    replace = 1 + cache[idx1 + 1][idx2 + 1]
                    cache[idx1][idx2] = min(insert, delete, replace)

        return cache[0][0]
```

Now, you can notice that to compute the row, we just need the previous one. So we can optimize this solution to have just `O(m)` space complexity.