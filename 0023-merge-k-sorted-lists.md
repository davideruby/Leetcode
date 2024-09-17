## [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

<h2 style="color:#ff375f">Hard</h2>
You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

## Solution
```python
class Solution:
    def mergeKLists(self, lists: List[Optional[ListNode]]) -> Optional[ListNode]:
        if len(lists) == 0: 
            return None
        return self.mergeKListsHelper(lists, 0, len(lists) - 1)


    def mergeKListsHelper(self, lists: List[Optional[ListNode]], start: int, end: int) -> Optional[ListNode]:
        if start == end:
            return lists[start]

        middle = (end + start) // 2
        left = self.mergeKListsHelper(lists, start, middle)
        right = self.mergeKListsHelper(lists, middle + 1, end)
        return self.merge(left, right)


    def merge(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        merged = ListNode(0)
        node = merged

        while list1 and list2:
            if list1.val < list2.val:
                node.next = list1
                list1 = list1.next
            else:
                node.next = list2
                list2 = list2.next

            node = node.next

        if list1:
            node.next = list1
        if list2:
            node.next = list2

        return merged.next
```

## Notes
If you use the logic of the merge sort, you can achieve a time complexity of O(nlogk).