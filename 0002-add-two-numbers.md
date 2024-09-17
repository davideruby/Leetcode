## [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

<h2 style="color:#fac31d">Medium</h2>
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

## Solution
```python
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        result = ListNode() # add a dummy node just to make the insertion of new nodes easier
        node = result
        carry = 0

        while l1 or l2:
            l1_val = l1.val if l1 else 0
            l2_val = l2.val if l2 else 0

            val_sum = l1_val + l2_val + carry
            carry = val_sum // 10
            val_sum = val_sum % 10

            node.next = ListNode(val_sum, None)
            node = node.next

            if l1:
                l1 = l1.next
            if l2:
                l2 = l2.next

        if carry > 0:
            node.next = ListNode(carry, None)

        return result.next
```

## Notes
Think how we solved at elementary school the sum of two numbers.