## [2185. Counting Words With a Given Prefix](https://leetcode.com/problems/counting-words-with-a-given-prefix/)

${\textsf{\color{green}Easy}}$

You are given an array of strings words and a string pref.

Return the number of strings in words that contain pref as a prefix.

A prefix of a string s is any leading contiguous substring of s.

## Solution
```python
class Solution:
    def prefixCount(self, words: List[str], pref: str) -> int:
        count = 0
        for word in words:
            if pref == word[:len(pref)]:
                count += 1
        return count
```

## Notes
The trivial solution is efficient and it takes `O(n * m)` time complexity, where `n` is the length of words and `m` the length of `pref`.

Just for exercise purpose, below I put a solution using a variation of the `Trie` data structure:
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.count = 0

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def add(self, word):
        node = self.root

        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            
            node = node.children[char]
            node.count += 1

    def countPrefix(self, prefix):
        node = self.root

        for char in prefix:
            if char not in node.children:
                return 0
            node = node.children[char]
        
        return node.count

class Solution:
    def prefixCount(self, words: List[str], pref: str) -> int:
        trie = Trie()

        for word in words:
            trie.add(word)

        return trie.countPrefix(pref)
```
