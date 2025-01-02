## [2559. Count Vowel Strings in Ranges](https://leetcode.com/problems/count-vowel-strings-in-ranges/)

${\textsf{\color{yellow}Medium}}$

You are given a 0-indexed array of strings words and a 2D array of integers queries.

Each query queries[i] = [li, ri] asks us to find the number of strings present in the range li to ri (both inclusive) of words that start and end with a vowel.

Return an array ans of size queries.length, where ans[i] is the answer to the ith query.

Note that the vowel letters are 'a', 'e', 'i', 'o', and 'u'.

## Solution
```python
class Solution:
    def vowelStrings(self, words: List[str], queries: List[List[int]]) -> List[int]:
        vowels = set(['a', 'e', 'i', 'o', 'u'])
        
        prefix = [0] * (len(words) + 1)
        for idx, word in enumerate(words):
            prefix[idx] = prefix[idx - 1]
            if word[0] in vowels and word[-1] in vowels:
                prefix[idx] += 1

        ans = []
        for left, right in queries:
            ans.append(prefix[right] - prefix[left - 1])
    
        return ans
```

## Notes
Precompute the prefix sum of strings that start and end with vowels.
