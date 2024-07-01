## [133. Clone Graph](https://leetcode.com/problems/clone-graph/)

<h2 style="color:#fac31d">Medium</h2>

Given a reference of a node in a connected undirected graph.

Return a deep copy (clone) of the graph.

## Solution
```python
from typing import Optional

class Solution:
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:
        if node == None:
            return None

        return self.copy_dfs(node, {})
        return self.copy_bfs(node)
    

    def copy_bfs(self, node: Optional['Node']) -> Optional['Node']:
        queue = deque([node])
        copies = { node : Node(node.val)}

        while queue:
            for _ in range(len(queue)):
                curr = queue.popleft()

                for neighbor in curr.neighbors:
                    if neighbor not in copies:
                        copies[neighbor] = Node(neighbor.val)
                        queue.append(neighbor)
                    copies[curr].neighbors.append(copies[neighbor])
        
        return copies[node]


    def copy_dfs(self, node: Optional['Node'], copies: Dict[Optional['Node'], Optional['Node']]) -> Optional['Node']:
        copies[node] = Node(node.val)

        for neighbor in node.neighbors:
            if neighbor not in copies:
                self.copy_dfs(neighbor, copies)
            copies[node].neighbors.append(copies[neighbor])
        
        return copies[node]
```

## Notes
Traverse the graph (through a bfs or a dfs) and use hashmap to map each node to its respective copy.
Each time you deal with a neighbor, if the copy is already in the hashmap, use that, otherwise create a new Node.
I provide both the solution with dfs and bfs.
