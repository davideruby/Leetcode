## [2130. Maximum Twin Sum of a Linked List](https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list/)

<h2 style="color:#fac31d">Medium</h2>
In a linked list of size n, where n is even, the ith node (0-indexed) of the linked list is known as the twin of the (n-1-i)th node, if 0 <= i <= (n / 2) - 1.

For example, if n = 4, then node 0 is the twin of node 3, and node 1 is the twin of node 2. These are the only nodes with twins for n = 4.
The twin sum is defined as the sum of a node and its twin.

Given the head of a linked list with even length, return the maximum twin sum of the linked list.

## Solution
```python
class Solution:
    def pairSum(self, head: Optional[ListNode]) -> int:
        # find the middle
        slow = head
        fast = head.next
        while fast.next != None:
            slow = slow.next
            fast = fast.next.next

        # reverse the second half of the list
        node = slow.next
        prev = None
        while node != None:
            next_node = node.next
            node.next = prev
            prev = node
            node = next_node

        # get max twin sum
        twin1 = prev
        twin2 = head
        max_twin_sum = 0
        while twin1 != None:
            twin_sum = twin1.val + twin2.val
            if twin_sum > max_twin_sum:
                max_twin_sum = twin_sum

            twin1 = twin1.next
            twin2 = twin2.next

        return max_twin_sum
```

## Notes
Get the middle node with slow and fast pointer. Reverse the second half of the list. Get the max twin sum.
