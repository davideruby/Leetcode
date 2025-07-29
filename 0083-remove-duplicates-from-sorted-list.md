## [83. Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/)

${\textsf{\color{green}Easy}}$

Given the head of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.

## Solution
```python
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        node = head

        while node:
            if node.next and node.val == node.next.val:
                node.next = node.next.next
            else:
                node = node.next

        return head
```
