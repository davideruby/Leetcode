## [211. Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/)

<h2 style="color:#fac31d">Medium</h2>
Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the WordDictionary class:

- WordDictionary() Initializes the object.
- void addWord(word) Adds word to the data structure, it can be matched later.
- bool search(word) Returns true if there is any string in the data structure that matches word or false otherwise. word may contain dots '.' where dots can be matched with any letter.

## Solution
```python
class WordDictionaryNode:

    def __init__(self):
        self.children = {}
        self.end_of_word = False


class WordDictionary:

    def __init__(self):
        self.root = WordDictionaryNode()


    def addWord(self, word: str) -> None:
        node = self.root

        for char in word:
            if char not in node.children:
                node.children[char] = WordDictionaryNode()
            node = node.children[char]

        node.end_of_word = True
        

    def search(self, word: str) -> bool:
        return self._searchOnNode(self.root, word)

    
    def _searchOnNode(self, node: WordDictionaryNode, word: str) -> bool:
        for idx, char in enumerate(word):
            if char != ".":
                if char not in node.children:
                    return False
                node = node.children[char]
            else:
                sub_word = word[idx + 1:]
                for child in node.children.values():
                    if self._searchOnNode(child, sub_word):
                        return True
                return False
        
        return node.end_of_word
```

## Notes
You should be familiar with how a Trie works.

The `search()` method calls a helper function `_searchOnNode()`. If the current character is not a dot, the search method is basically the same as the `search()` method of a traditional Trie. Otherwise, if the current character is a dot, we have to perform a brute force approach in which we recursively search in every child of the current node.
