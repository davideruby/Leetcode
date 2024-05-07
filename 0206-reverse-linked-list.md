## [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

<h2 style="color:#00b8a3">Easy</h2>
Given the head of a singly linked list, reverse the list, and return the reversed list.

## Solution
```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current = head
        prev = None

        while current != None:
            next_node = current.next
            current.next = prev
            prev = current
            current = next_node

        return prev
```

## Notes
The idea is the following: initialize `current = head` and `prev = None`. At each iteration: 1. `next_node = node.next` 2. `node.next = prev` 3. `prev = node` 4. `node = next_node`.
