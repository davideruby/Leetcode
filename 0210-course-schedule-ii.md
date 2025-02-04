## [210. Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)

${\textsf{\color{yellow}Medium}}$

There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

- For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.

Return the ordering of courses you should take to finish all courses. If there are many valid answers, return any of them. If it is impossible to finish all courses, return an empty array.

## Solution
```python
class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        graph = self.buildGraph(numCourses, prerequisites)
        return self.topologicalSort(graph)

    def buildGraph(self, numCourses: int, prerequisites: List[List[int]]) -> Dict[int, List[int]]:
        graph = { course: [] for course in range(numCourses) }

        for course, prereq in prerequisites:
            graph[course].append(prereq)

        return graph

    def topologicalSort(self, graph: Dict[int, List[int]]) -> List[int]:
        visited = set()
        order = []
        for course in graph.keys():
            if not self.dfs(graph, course, visited, set(), order):
                return []

        return order

    def dfs(self, graph: Dict[int, List[int]], course: int, visited: Set[int], cycle: Set[int], order: List[int]) -> bool:
        if course in cycle:
            return False
        if course in visited:
            return True

        visited.add(course)
        cycle.add(course)
        for prereq in graph[course]:
            if not self.dfs(graph, prereq, visited, cycle, order):
                return False
        
        cycle.remove(course)
        order.append(course)
        return True
```

## Notes
Build the graph and perform a topological sort. While performing the topological sort, check the graph does not contain a cycle.
