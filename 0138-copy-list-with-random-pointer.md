## [138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/)

<h2 style="color:#fac31d">Medium</h2>
A linked list of length n is given such that each node contains an additional random pointer, which could point to any node in the list, or null.

Construct a deep copy of the list. The deep copy should consist of exactly n brand new nodes, where each new node has its value set to the value of its corresponding original node. Both the next and random pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. None of the pointers in the new list should point to nodes in the original list.

For example, if there are two nodes X and Y in the original list, where X.random --> Y, then for the corresponding two nodes x and y in the copied list, x.random --> y.

Return the head of the copied linked list.

The linked list is represented in the input/output as a list of n nodes. Each node is represented as a pair of [val, random_index] where:

- val: an integer representing Node.val
- random_index: the index of the node (range from 0 to n-1) that the random pointer points to, or null if it does not point to any node.

Your code will only be given the head of the original linked list.

## Solution
```python
class Solution:
    # first solution, O(n) time, O(n) space
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        node_map = { None: None }
        node = head
        while node != None:
            node_map[node] = Node(node.val)
            node = node.next

        node = head
        while node != None:
            node_map[node].next = node_map[node.next]
            node_map[node].random = node_map[node.random]
            node = node.next

        return node_map[head]

    # second solution, O(n) time, O(1) space
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        if head == None:
            return None

        node = head
        while node != None:
            node.next = Node(node.val, node.next, node.random)
            node = node.next.next

        node = head.next
        while node != None:
            if node.random != None:
                node.random = node.random.next
            if node.next != None:
                node.next = node.next.next
            node = node.next

        return head.next
```

## Notes
- First solution is to have a hashmap, in which each original node is mapped to its copy. Then, in order to set .next and .random of copied nodes, we just do: `old_to_copy[node].next = old_to_copy[node.next]; old_to_copy[node].random = old_to_copy[node.random]`
- Second solution is to insert the copy of each node right next to it. Then set correctly the next and random pointers. This solution has a better space complexity but destroys the original list
