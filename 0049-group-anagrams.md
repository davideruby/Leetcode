## [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/)

<h2 style="color:#fac31d">Medium</h2>
Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Solution
```python
class Solution:
    def signature(self, string):
        len_signature = ord('z') - ord('a') + 1
        count_chars = [0] * len_signature
        for char in string:
            count_chars[ord(char) - ord('a')] += 1

        signature = ""
        for char_ord in range(ord('a'), ord('z') + 1):
            signature += chr(char_ord) * count_chars[char_ord - ord('a')]
        return signature

    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        anagrams = {}

        for string in strs:
            signature = self.signature(string)
            if signature not in anagrams:
                anagrams[signature] = []
            anagrams[signature].append(string)

        return anagrams.values()
```

## Notes
For each string build a ordered signature made of every character in it. For example the signature of `"zdwwaa"` is `"aadwwz"`. Then group in a map each string by its signature.
