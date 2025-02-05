## [269. Alien Dictionary](https://leetcode.com/problems/alien-dictionary)

${\textsf{\color{red}Hard}}$

There is a foreign language which uses the latin alphabet, but the order among letters is not "a", "b", "c" ... "z" as in English.

You receive a list of non-empty strings words from the dictionary, where the words are sorted lexicographically based on the rules of this new language.

Derive the order of letters in this language. If the order is invalid, return an empty string. If there are multiple valid order of letters, return any of them.

A string a is lexicographically smaller than a string b if either of the following is true:

- The first letter where they differ is smaller in a than in b.
- There is no index i such that a[i] != b[i] and a.length < b.length.

## Solution
```python
class Solution:
    def alienDictionary(self, words: List[str]) -> str:
        try:
            graph = self.buildGraph(words)
            return ''.join(self.topologicalSort(graph))
        except:
            return '' # invalid input

    def buildGraph(self, words):
        graph = {}

        for word in words:
            for char in word:
                graph[char] = set()

        for idx in range(len(words) - 1):
            word1 = words[idx]
            word2 = words[idx + 1]
            min_len = min(len(word1), len(word2))

            if len(word1) > len(word2) and word1[:min_len] == word2[:min_len]:
                raise "invalid input"

            for idx_char in range(min_len):
                if word1[idx_char] != word2[idx_char]:
                    graph[word1[idx_char]].add(word2[idx_char])
                    break

        return graph

    def topologicalSort(self, graph):
        visited = set()
        order = []

        for node in graph:
            if not self.dfs(graph, node, visited, set(), order):
                raise "cycled graph"
        
        return reversed(order)

    def dfs(self, graph, node, visited, cycle, order):
        if node in cycle:
            return False

        if node in visited:
            return True

        visited.add(node)
        cycle.add(node)
        for neighbor in graph[node]:
            if not self.dfs(graph, neighbor, visited, cycle, order):
                return False

        cycle.remove(node)
        order.append(node)
        return True
```

## Notes
Let's suppose this input: `["hrn","hrf","er","enn","rfnn"]`:
- from "hrn" and "hrf", we know 'n' < 'f'
- from "hrf" and "er", we know 'h' < 'e'
- from "er" and "enn", we know get 'r' < 'n'
- from "enn" and "rfnn" we know 'e' < 'r'

So, what about building the graph `h ---> e ---> r ---> n --> f` and return the topological sort?

