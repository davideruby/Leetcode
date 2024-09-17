## [876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)

<h2 style="color:#00b8a3">Easy</h2>

Given the head of a singly linked list, return the middle node of the linked list.
If there are two middle nodes, return the second middle node.

## Solution
```python
class Solution:
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow = head
        fast = head

        while fast != None and fast.next != None:
            fast = fast.next.next
            slow = slow.next

        return slow
```

## Notes
Slow and Fast Pointer (Floyd's tortoise and hare algorithm).
