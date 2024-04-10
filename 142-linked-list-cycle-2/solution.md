# 1st step
- 途中までループが開始するLinkedListの番号を返すと問題文を読み間違えていたのでDictで実装してしまった
- setを使えばよかった
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        visitedIndex = dict()
        counter = 0
        while head:
            if head in visitedIndex:
                return head
            visitedIndex[head] = counter
            counter += 1
            head = head.next
        return None    
```
# 2nd step
- setに訪れたことのあるNodeを追加していく
- 今のノードがsetにあったら現在地点を返す
``` python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        visitedNodes = set()
        while head:
            if head in visitedNodes:
                return head
            visitedNodes.add(head)
            head = head.next
        return None
```
# 3rd step
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        visitedNodes = set()
        while head:
            if head in visitedNodes:
                return head
            visitedNodes.add(head)
            head = head.next
        return None
```