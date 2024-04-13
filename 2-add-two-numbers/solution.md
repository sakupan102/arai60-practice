# 1st 
```python
- l1とl2を見てtail_pointerに値を追加していく
- carryフラグを用いて繰上りを管理した
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        added_list = ListNode()
        tail_pointer = added_list
        carry = 0
        while l1 or l2:
            added_val = carry
            if l1 != None:
                added_val += l1.val
                l1 = l1.next
            if l2 != None:
                added_val += l2.val
                l2 = l2.next
            if added_val >= 10:
                carry = 1
                tail_pointer.next = ListNode(added_val - 10)
            else:
                carry = 0
                tail_pointer.next = ListNode(added_val)
            tail_pointer = tail_pointer.next
        if carry == 1:
            tail_pointer.next = ListNode(carry)
        return added_list.next
```
# 2nd
- divmod関数を使ってcarryが生じたときの処理を一つにまとめた
- https://discord.com/channels/1084280443945353267/1200089668901937312/1206949445359640576
    - 値を可算する処理とl1, l2のheadを移動させる処理は別の場所でやってもいいかもしれない
- https://discord.com/channels/1084280443945353267/1196472827457589338/1197166381146329208
    - 再帰で書くこともできる
    - ループの方が可読性が高い??
- https://discord.com/channels/1084280443945353267/1199984201521430588/1200190786357186580
    - while文内にcarryに関する条件を入れてwhile文終了後のcarryに関する処理を削減してもいいかも
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        added_list = ListNode(-1000)
        tail_pointer = added_list
        carry = 0
        while l1 or l2:
            added_val = carry
            if l1 != None:
                added_val += l1.val
                l1 = l1.next
            if l2 != None:
                added_val += l2.val
                l2 = l2.next
            carry, digit = divmod(added_val, 10)
            tail_pointer.next = ListNode(digit)
            tail_pointer = tail_pointer.next
        if carry == 1:
            tail_pointer.next = ListNode(1)
        return added_list.next
```
# 3rd
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        added_list = ListNode()
        tail_pointer = added_list
        carry = 0
        while l1 or l2 or carry:
            added_val = carry
            if l1:
                added_val += l1.val
                l1 = l1.next
            if l2:
                added_val += l2.val
                l2 = l2.next
            carry, digit = divmod(added_val, 10)
            tail_pointer.next = ListNode(digit)
            tail_pointer = tail_pointer.next
        return added_list.next
```