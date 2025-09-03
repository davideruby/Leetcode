## [203. Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/)

${\textsf{\color{green}Easy}}$

Given the head of a linked list and an integer val, remove all the nodes of the linked list that has Node.val == val, and return the new head.

## Solution
```python
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        while head and head.val == val:
            head = head.next

        node = head
        while node:
            while node.next and node.next.val == val:
                node.next = node.next.next
            node = node.next
        
        return head
```
