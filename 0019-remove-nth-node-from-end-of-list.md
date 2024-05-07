## [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

<h2 style="color:#fac31d">Medium</h2>
Given the head of a linked list, remove the nth node from the end of the list and return its head.

## Solution
```python
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(0, head)
        left = dummy
        right = head
        idx = 0
        removed = False

        while not removed:
            if right != None:
                right = right.next
                idx += 1

            if idx > n:
                left = left.next

            if right == None:
                left.next = left.next.next
                removed = True

        return dummy.next
```

## Notes
Maintain two pointers and update one with a delay of n steps. When the right pointer reaches the end, delete the node.
