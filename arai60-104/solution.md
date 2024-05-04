# 1st
- 再帰DFSで解いた
```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        right_depth = self.maxDepth(root.right)
        left_depth = self.maxDepth(root.left)
        return max(right_depth, left_depth) + 1
```
# 2nd
- スタックを積むタイプのDFSで解いた。
- https://github.com/Mike0121/LeetCode/pull/6/files
  - これの1回目、nodesとnextNodesを用いてBFS的にも解ける。
- https://github.com/hayashi-ay/leetcode/pull/22/files
- dequeを用いてBFSもできるがデータ構造的に単純なstack DFSのほうが効率がよさそう
```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        node_and_depth = [(root, 1)]
        max_depth = 1
        while node_and_depth:
            node, depth = node_and_depth.pop()
            max_depth = max(max_depth, depth)
            if node.right:
                node_and_depth.append((node.right, depth + 1))
            if node.left:
                node_and_depth.append((node.left, depth + 1))
        return max_depth
```
# 3rd
```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        left_depth = self.maxDepth(root.left)
        right_depth = self.maxDepth(root.right)
        return max(left_depth, right_depth) + 1
```
