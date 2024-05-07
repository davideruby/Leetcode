## [146. LRU Cache](https://leetcode.com/problems/lru-cache/)

<h2 style="color:#fac31d">Medium</h2>
Design a data structure that follows the constraints of a Least Recently Used (LRU) cache.

Implement the LRUCache class:

- LRUCache(int capacity) Initialize the LRU cache with positive size capacity.
- int get(int key) Return the value of the key if the key exists, otherwise return -1.
- void put(int key, int value) Update the value of the key if the key exists. Otherwise, add the key-value pair to the cache. If the number of keys exceeds the capacity from this operation, evict the least recently used key.

The functions get and put must each run in O(1) average time complexity.

## Solution
```python
class Node:

    def __init__(self, key: int, value: int, prev=None, next=None):
        self.key = key
        self.value = value
        self.prev = prev
        self.next = next


class LRUCache:

    def __init__(self, capacity: int):
        self.capacity = capacity
        self.cache = { }
        self.left = Node(0, 0)
        self.right = Node(0, 0)
        self.left.next = self.right
        self.right.prev = self.left


    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1

        self.remove(self.cache[key])
        self.insert(self.cache[key])
        return self.cache[key].value


    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            self.remove(self.cache[key])

        self.cache[key] = Node(key, value)
        self.insert(self.cache[key])
        if len(self.cache) > self.capacity:
            lru = self.lru()
            self.remove(lru)
            del self.cache[lru.key]


    def insert(self, node: Node) -> None:
        node.next = self.right
        node.prev = self.right.prev
        self.right.prev.next = node
        self.right.prev = node


    def remove(self, node: Node) -> None:
        node.prev.next = node.next
        node.next.prev = node.prev


    def lru(self) -> Node:
        return self.left.next
```

## Notes
Very hard to solve if you have never seen it before. Probably the real complexity should be hard. 
The idea of the solution is to use a doubly linked list, where the least recently used element is the one at the head of the list.
