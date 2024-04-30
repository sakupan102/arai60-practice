# 1st 
- ListNodeを右に延長する方法に手こずった
- 左に延長なら簡単で`nodes = ListNode(newVal, nodes)`とかすればいい
- 右に延長するために右端のノードを指すポインタ`removed_list_pointer`を使った
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head:
            return None
        removed_list = ListNode(head.val, None)
        removed_list_pointer = removed_list
        current_val = head.val
        head = head.next
        while head:
            if head.val == current_val:
                head = head.next
                continue
            removed_list_pointer.next = ListNode(head.val)
            current_val = head.val
            head = head.next
            removed_list_pointer 
        return removed_list
```
# 2nd 
- 再帰で実装した方が見やすそうだったのでやってみた
- 47 - 49のコードが50 - 52のコードとほぼ一緒なので一つにまとめたかったができなかった...
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head:
            return None
        def remove_duplicates(head, current_val):
            if not head:
                return None
            if head.val == current_val:
                return remove_duplicates(head.next, current_val)
            current_val = head.val
            nodes = remove_duplicates(head.next, current_val)
            return ListNode(head.val, nodes)
        val = head.val
        without_duplicate = remove_duplicates(head.next, val)
        return ListNode(val, without_duplicate)
```
# 3rd
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head:
            return None
        def remove_duplicate(head, current_val):
            if not head:
                return None
            if head.val == current_val:
                return remove_duplicate(head.next, current_val)
            current_val = head.val
            without_duplicate = remove_duplicate(head.next, current_val)
            return ListNode(current_val, without_duplicate)
        current_val = head.val
        without_duplicate = remove_duplicate(head.next, current_val)
        return ListNode(current_val, without_duplicate)
```