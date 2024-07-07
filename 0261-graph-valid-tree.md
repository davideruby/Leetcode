## [261. Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree/)

<h2 style="color:#fac31d">Medium</h2>

Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree.

## Solution
```python
class Solution:
    def validTree(self, n: int, edges: List[List[int]]) -> bool:
        graph = self.buildUndirectedGraph(edges)
        return self.graphIsTree(graph)
        

    def buildUndirectedGraph(self, edges: List[List[int]]) -> Dict[int, List[int]]:
        graph = {}
        
        for source, dest in edges:
            if source not in graph:
                graph[source] = []
            if dest not in graph:
                graph[dest] = []
            graph[source].append(dest)
            graph[dest].append(source)
        
        return graph


    def graphIsTree(self, graph: Dict[int, List[int]]) -> bool:
        if len(graph) == 0:
            return True

        visited = set()
        is_cyclic = self.isCyclic(graph, 0, -1, visited)
        all_nodes_visited = len(visited) == len(graph.keys())
        return not is_cyclic and all_nodes_visited

    
    def isCyclic(self, graph: Dict[int, List[int]], node: int, parent: int, visited: set[int]) -> bool:
        visited.add(node)

        for neighbor in graph[node]:
            if neighbor not in visited:
                if self.isCyclic(graph, neighbor, node, visited):
                    return True
            elif neighbor != parent:
                return True
            
        return False
```

## Notes
First of all, build an undirected graph from the edges.

Then, perform a depth-first search of the graph to check if it is a valid tree. In each step, pass to the current node the parent (the previous node). If a node has a neighbour which is already visited and is not its parent, it means we detected a cycle in the graph, i.e. the graph is not a tree.

Besides, if the depth-first search has not visited all the nodes, it means we have more than one connected components in the graph, that said the graph is not a valid tree.
