## [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

<h2 style="color:#00b8a3">Easy</h2>

Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.

## Solution
```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow = head
        fast = head

        while fast != None and fast.next != None:
            fast = fast.next.next
            slow = slow.next

            if fast == slow:
                return True

        return False
```

## Notes
Slow and Fast Pointer (Floyd's tortoise and hare algorithm).
