# 1st step
- 83と同じで再帰で実装
- 再帰にはremoved_numを引数にとっておりこれは
    - 重複が生じているか
    - 生じているならどの番号で起きているか
を表している
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        def remove_duplicate(head, remove_num):
            if not head:
                return None
            if head.val == remove_num:
                return remove_duplicate(head.next, remove_num)
            if not head.next:
                return head
            if head.val == head.next.val:
                return remove_duplicate(head.next, head.val)
            without_duplicate = remove_duplicate(head.next, None)
            return ListNode(head.val, without_duplicate)
        return remove_duplicate(head, None)
```
# 2nd step
- 再帰よりもループのほうが可読性が高いようなのでループで実装
- 重複しているノードをスキップする関数skip_duplicateを追加
- skip_duplicateを関数内部に定義しているがメンバ関数として定義した方が良い？？
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        def skip_duplicate(current):
            while current.next and (current.val == current.next.val):
                current = current.next
            current = current.next
            return current
        dummy_head = ListNode(-1000, head)
        tail_pointer = dummy_head
        current = head
        while current:
            if (not current.next) or (current.val != current.next.val):
                tail_pointer.next = current
                tail_pointer = current
                current = current.next
            else:
                current = skip_duplicate(current)
        tail_pointer.next = current
        return dummy_head.next        
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
        def skip_duplicate(head):
            while head.next and (head.val == head.next.val):
                head = head.next
            return head.next
        dummy_head = ListNode(-1000, head)
        tail_pointer = dummy_head
        current = head
        while current:
            if (not current.next) or (current.val != current.next.val):
                tail_pointer.next = current
                tail_pointer = current
                current = current.next
            else:
                current = skip_duplicate(current)
        tail_pointer.next = current
        return dummy_head.next
```