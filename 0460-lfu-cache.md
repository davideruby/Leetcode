## [460. LFU Cache](https://leetcode.com/problems/lfu-cache/)

${\textsf{\color{red}Hard}}$

Design and implement a data structure for a Least Frequently Used (LFU) cache.

Implement the LFUCache class:

- LFUCache(int capacity) Initializes the object with the capacity of the data structure.
- int get(int key) Gets the value of the key if the key exists in the cache. Otherwise, returns -1.
- void put(int key, int value) Update the value of the key if present, or inserts the key if not already present. When the cache reaches its capacity, it should invalidate and remove the least frequently used key before inserting a new item. For this problem, when there is a tie (i.e., two or more keys with the same frequency), the least recently used key would be invalidated.
To determine the least frequently used key, a use counter is maintained for each key in the cache. The key with the smallest use counter is the least frequently used key.

When a key is first inserted into the cache, its use counter is set to 1 (due to the put operation). The use counter for a key in the cache is incremented either a get or put operation is called on it.

The functions get and put must each run in O(1) average time complexity.

## Solution
```python
class ListNode:
    def __init__(self, val: int, prev=None, next=None):
        self.val = val
        self.prev = prev
        self.next = next

class LinkedList:
    def __init__(self):
        self.left = ListNode(0)
        self.right = ListNode(0)
        self.left.next = self.right
        self.right.prev = self.left
        self.nodeMap = {}

    def __len__(self):
        return len(self.nodeMap)

    def pushRight(self, val):
        node = ListNode(val, self.right.prev, self.right)
        self.right.prev.next = node
        self.right.prev = node
        self.nodeMap[val] = node

    def pop(self, val):
        if val not in self.nodeMap:
            return
        
        node = self.nodeMap[val]
        node.prev.next = node.next
        node.next.prev = node.prev
        self.nodeMap.pop(val)

    def popLeft(self):
        popped = self.left.next.val
        self.pop(popped)
        return popped
        

class LFUCache:

    def __init__(self, capacity: int):
        self.capacity = capacity
        self.lfuCount = 0
        self.map = {}
        self.listMap = defaultdict(LinkedList)
        self.counts = defaultdict(int)

    def incrementCounter(self, key):
        count = self.counts[key]
        self.listMap[count].pop(key)
        self.listMap[count + 1].pushRight(key)

        self.counts[key] += 1

        if self.lfuCount == count and len(self.listMap[count]) == 0:
            self.lfuCount += 1
        

    def get(self, key: int) -> int:
        if key not in self.map:
            return -1

        self.incrementCounter(key)
        return self.map[key]

    def put(self, key: int, value: int) -> None:
        if self.capacity == 0:
            return

        if key not in self.map and len(self.map) == self.capacity:
            removed = self.listMap[self.lfuCount].popLeft()
            self.map.pop(removed)
            self.counts.pop(removed)

        self.incrementCounter(key)
        self.map[key] = value

        self.lfuCount = min(self.lfuCount, self.counts[key])
```

## Notes
This solution is built on top of the [146. LRU Cache](./0146-lru-cache.md). As the LRU cache, we use a doubly linked list, where the first element is the least recently used and the last element is the most recently used.

Then, in the LFU cache, we use a hashmap, where they key is an integer count and the value a linked list. The key of the map represents the number of times the key has been used.

Suppose we call `get(key)`, where key has been used `count` times. So, we pop key from the list of `count` and add it to to the right of the list of `count + 1`. If now the list of `count` is empty and the `lfuCount` is equal to it, now the new `lfuCount` will be `count + 1`.

When we call `put(key, value)`, if the LFU cache is full, we pop the LRU element from the list of `lfuCount`.
