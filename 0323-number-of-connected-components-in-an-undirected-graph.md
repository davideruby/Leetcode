## [323. Number of Connected Components In An Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/)

<h2 style="color:#fac31d">Medium</h2>

There is an undirected graph with n nodes. There is also an edges array, where edges[i] = [a, b] means that there is an edge between node a and node b in the graph.

Return the total number of connected components in that graph.

## Solution
```python
class Solution:
    def countComponents(self, n: int, edges: List[List[int]]) -> int:
        graph = self.buildGraph(n, edges)

        visited = set()
        count = 0
        for node in range(n):
            if node not in visited:
                count += 1
                self.dfs(graph, node, visited)
        
        return count


    def buildGraph(self, n: int, edges: List[List[int]]) -> Dict[int, List[int]]:
        graph = { node: [] for node in range(n) }
        
        for source, dest in edges:
            graph[source].append(dest)
            graph[dest].append(source)

        return graph

    
    def dfs(self, graph: Dict[int, List[int]], node: int, visited: set[int]) -> None:
        visited.add(node)

        for neighbor in graph[node]:
            if neighbor not in visited:
                self.dfs(graph, neighbor, visited)
```

## Notes
When you perform a dfs on the graph, you keep track of visited notes through a hashset.
To discover the number of connected components, loop over each node of the graph, and perform a dfs starting from that node if it is not still visited.