# 1st
―inplaceで解く方法とあたらしくListNodeを作る二つの方法が考えられる
## inplaceの回答
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        reversed_list = None
        while head:
            reversed_list = ListNode(head.val, reversed_list)
            head = head.next
        return reversed_list
```
## inplaceじゃない方
- tail_headという変数名は変えた方がいい
- while文内`if not next_node`もどうにかしたい
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head:
            return None
        tail_head = None
        current = head
        next_node = head.next
        while current:
            current.next = tail_head
            tail_head = current
            current = next_node 
            if not next_node:
                break
            next_node = next_node.next
        return tail_head
```
# 2nd
- 2ndからはinplaceの回答のみにする
- https://discord.com/channels/1084280443945353267/1200089668901937312/1204756236973776916
    - 再帰でも書ける
    - https://github.com/python/cpython/pull/28488/files
      - この最適化でスタックを積まずに再帰関数が呼べる
- https://github.com/cheeseNA/leetcode/pull/11
    - テンポラリーのポインターをwhile文内で定義することで最初の`if not head`を削減している
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        reversed_list = None
        current = head
        while current:
            next_pointer = current.next
            current.next = reversed_list
            reversed_list = current
            current = next_pointer
        return reversed_list
```
# 3rd
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        reversed_list = None
        current = head
        while current:
            next_pointer = current.next
            current.next = reversed_list
            reversed_list = current
            current = next_pointer
        return reversed_list
```