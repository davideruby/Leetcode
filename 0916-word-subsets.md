## [916. Word Subsets](https://leetcode.com/problems/word-subsets/)

${\textsf{\color{yellow}Medium}}$

You are given two string arrays words1 and words2.

A string b is a subset of string a if every letter in b occurs in a including multiplicity.

- For example, "wrr" is a subset of "warrior" but is not a subset of "world".

A string a from words1 is universal if for every string b in words2, b is a subset of a.

Return an array of all the universal strings in words1. You may return the answer in any order.

## Solution
```python
class Solution:
    def wordSubsets(self, words1: List[str], words2: List[str]) -> List[str]:
        max_freq = {}
        for word in words2:
            signature = self.getSignature(word)
            for char, count in signature.items():
                max_freq[char] = max(max_freq.get(char, 0), count)
        
        universals = []
        for word in words1:
            signature = self.getSignature(word)
            is_universal = all([signature.get(char, 0) >= count for char, count in max_freq.items()])
            if is_universal:
                universals.append(word)
        
        return universals


    def getSignature(self, word: str) -> Dict[str, int]:
        signature = {}

        for char in word:
            signature[char] = signature.get(char, 0) + 1
        
        return signature
```

## Notes
In order to check if a string is a subset of another string, the easiest way is by using hashmaps, where the key is the character of the string and the value is the number of times the char appears in the string.

The tricky point of this problem is that you can merge all the hashmaps of the array `words2` to get a single hashmaps of size `26` (the number of characters between `a-z`).
In this way we can dramatically reduce the time complexity. This solution solves the problem with a time complexity of `O(n * max2 + m * max1 * 26)`, where:
- `n` is the size of `words2`,
- `max2` is the length of the longest string in `words2`,
- `m` is the size of `words1`,
- `max1` is the length of the longest string in `words1`,
- `26` is the length of the merged hashmaps. Since it is a constant, you can delete it from the time complexity.
