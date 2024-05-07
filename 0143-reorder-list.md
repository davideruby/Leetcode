## [143. Reorder List](https://leetcode.com/problems/reorder-list)

<h2 style="color:#fac31d">Medium</h2>
You are given the head of a singly linked-list. The list can be represented as:

L0 → L1 → … → Ln - 1 → Ln
Reorder the list to be on the following form:

L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
You may not modify the values in the list's nodes. Only nodes themselves may be changed.

## Solution
```python
class Solution:
    def getMiddleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        fast = head.next
        slow = head
        while fast != None and fast.next != None:
            fast = fast.next.next
            slow = slow.next
        return slow

    def reverse(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        while head != None:
            next = head.next
            head.next = prev
            prev = head
            head = next
        return prev

    def merge(self, head1: Optional[ListNode], head2: Optional[ListNode]) -> None:
        while head1 != None and head2 != None:
            next_head1 = head1.next
            next_head2 = head2.next

            head1.next = head2
            head2.next = next_head1

            head1 = next_head1
            head2 = next_head2

    def reorderList(self, head: Optional[ListNode]) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        if head.next == None:
            return head

        end_first_half = self.getMiddleNode(head)
        head2 = self.reverse(end_first_half.next)
        end_first_half.next = None
        self.merge(head, head2)
```

## Notes
3 steps to success: 
1. Get the middle node of the list 
2. reverse the second half 
3. cut the first half and merge the two halves.
