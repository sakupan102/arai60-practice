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