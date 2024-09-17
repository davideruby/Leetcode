## [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

<h2 style="color:#00b8a3">Easy</h2>
You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

## Solution
```python
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        current = ListNode()
        merged_list = current

        while list1 and list2:
            if list1.val < list2.val:
                current.next = list1
                list1 = list1.next
            else:
                current.next = list2
                list2 = list2.next
            current = current.next

        if list1 == None:
            current.next = list2
        if list2 == None:
            current.next = list1

        return merged_list.next
```

## Notes
The easiest solution is to use a new dummy node. Then check the lower element between list1 and list2, and set `dummy.next` to it.