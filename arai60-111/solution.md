# 1st
- BFSで解いた
- dequeに`node == None`のやつも含めるか迷ったが、INFなどを使う必要がありそうだったので`node == None`は先頭で例外的に処理した。
```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def minDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        nodes_and_depth = deque([(root, 1)])
        while nodes_and_depth:
            node, depth = nodes_and_depth.popleft()
            if not node.left and not node.right:
                return depth
            if node.left:
                nodes_and_depth.append((node.left, depth + 1))
            if node.right:
                nodes_and_depth.append((node.right, depth + 1))
```
# 2nd
- stackを用いたBFSで解いた
  - doubly linked listを使ったdequeよりこちらの方がデータ構造的には単純
- https://github.com/hayashi-ay/leetcode/pull/26/files
  - minDepthが見つからなかったときに特定のエラーを出した方が良いかもしれない
  - 右と左にノードがあるかどうかの判定を関数で切り出してもよかった
```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def minDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        nodes = [root]
        depth = 0
        while nodes:
            depth += 1
            next_nodes = []
            for node in nodes:
                if not node.left and not node.right:
                    return depth
                if node.left:
                    next_nodes.append(node.left)
                if node.right:
                    next_nodes.append(node.right)
            nodes = next_nodess
```
# 3rd
```py
```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
from collections import deque
class Solution:
    def minDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        nodes = [root]
        depth = 0
        while nodes:
            depth += 1
            next_nodes = []
            for node in nodes:
                if not node.left and not node.right:
                    return depth
                if node.left:
                    next_nodes.append(node.left)
                if node.right:
                    next_nodes.append(node.right)
            nodes = next_nodess
```
