## [684. Redundant Connection](https://leetcode.com/problems/redundant-connection/)

${\textsf{\color{yellow}Medium}}$

In this problem, a tree is an undirected graph that is connected and has no cycles.

You are given a graph that started as a tree with n nodes labeled from 1 to n, with one additional edge added. The added edge has two different vertices chosen from 1 to n, and was not an edge that already existed. The graph is represented as an array edges of length n where edges[i] = [ai, bi] indicates that there is an edge between nodes ai and bi in the graph.

Return an edge that can be removed so that the resulting graph is a tree of n nodes. If there are multiple answers, return the answer that occurs last in the input.

## Solution
```python
class UnionFind:
    def __init__(self, num):
        self.parents = {}
        self.ranks = {}

        for idx in range(num):
            self.parents[idx] = idx
            self.ranks[idx] = 0

    def find(self, num):
        parent = self.parents[num]
        while parent != self.parents[parent]:
            self.parents[parent] = self.parents[self.parents[parent]]
            parent = self.parents[parent]
        return parent

    def union(self, num1, num2):
        parent1 = self.find(num1)
        parent2 = self.find(num2)

        if parent1 == parent2:
            return False

        if self.ranks[parent1] < self.ranks[parent2]:
            self.parents[parent1] = parent2
        elif self.ranks[parent1] > self.ranks[parent2]:
            self.parents[parent2] = parent1
        else:
            self.parents[parent1] = parent2
            self.ranks[parent1] += 1
        
        return True
    
class Solution:
    def findRedundantConnection(self, edges: List[List[int]]) -> List[int]:
        union_find = UnionFind(len(edges) + 1)

        for edge in edges:
            if not union_find.union(edge[0], edge[1]):
                return edge
```

## Notes
Solved with the UnionFind (aka disjoint sets) data structure. When two nodes are in different sets, their sets get united. When two nodes that are supposed to be united are already in the same set, it means that the edge between them is forming a cycle.
