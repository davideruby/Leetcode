## [142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)

<h2 style="color:#fac31d">Medium</h2>
Given the head of a linked list, return the node where the cycle begins. If there is no cycle, return null.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to (0-indexed). It is -1 if there is no cycle. Note that pos is not passed as a parameter.

Do not modify the linked list.

## Solution
```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head == None or head.next == None:
            return None

        slow = head
        fast = head

        while fast != None and fast.next != None:
            fast = fast.next.next
            slow = slow.next

            if fast == slow:
                break

        cycle = None
        cycle_found = fast == slow

        if cycle_found:
            cycle = head
            while cycle != slow:
                slow = slow.next
                cycle = cycle.next

        return cycle
```

## Notes
Slow and Fast Pointer (Floyd's tortoise and hare algorithm).
