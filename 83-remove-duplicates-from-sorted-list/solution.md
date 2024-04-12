# 1st step
- loopで再度実装
- current_valなどで値を保存せずに隣通しの値を見ることで処理を分けた
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        without_duplicate = head
        tail_pointer = without_duplicate
        while tail_pointer:
            if not tail_pointer.next:
                tail_pointer = tail_pointer.next
            elif tail_pointer.val == tail_pointer.next.val:
                tail_pointer.next = tail_pointer.next.next
            elif tail_pointer.val != tail_pointer.next.val:
                tail_pointer = tail_pointer.next
        return without_duplicate
```
# 2nd step
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current = head
        while current:
            if (not current.next) or (current.val != current.next.val):
                current = current.next
            else:
                current.next = current.next.next
        return head
```
# 3rd step
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current = head
        while current:
            if (not current.next) or (current.val != current.next.val):
                current = current.next
            else:
                current.next = current.next.next
        return head
```