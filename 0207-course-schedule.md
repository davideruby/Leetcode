## [207. Course Schedule](https://leetcode.com/problems/course-schedule/)

<h2 style="color:#fac31d">Medium</h2>

There are a total of numCourses courses you have to take, labeled from 0 to numCourses - 1. You are given an array prerequisites where prerequisites[i] = [ai, bi] indicates that you must take course bi first if you want to take course ai.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return true if you can finish all courses. Otherwise, return false.

## Solution
```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        graph = self.buildCoursesGraph(prerequisites)
        return not self.isGraphCyclic(graph)

    
    def buildCoursesGraph(self, prerequisites: List[List[int]]) -> Dict[int, List[int]]:
        graph = {}
        for course, prereq, in prerequisites:
            if course not in graph:
                graph[course] = []
            if prereq not in graph:
                graph[prereq] = []
            
            graph[prereq].append(course)
        
        return graph

    
    def isGraphCyclic(self, graph: Dict[int, List[int]]) -> bool:
        visited = set()
        path = set()
        for node in graph.keys():
            if self.cyclic(graph, node, visited, path):
                return True
        
        return False


    def cyclic(self, graph: Dict[int, List[int]], node: int, visited: set[int], path: set[int]) -> bool:
        if node in path:
            return True
        if node in visited:
            return False

        visited.add(node)
        path.add(node)
        for neighbor in graph[node]:
            if self.cyclic(graph, neighbor, visited, path):
                return True
        
        path.remove(node)
        return False
```

## Notes
The difficult aspect of this problem is to understand that the student can't finish all the courses if there is a cycle in the graph.
So, build a graph of the courses (prerequisites --> course) and check if that graph contains a cycle. 
