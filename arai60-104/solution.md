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

# stack + loopでの解法
```py
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:

        def set_left_depth(depth):
            parent = stack[-2]
            _, (_, left_right_depth) = parent
            left_right_depth[0] = depth
            return

        def set_right_depth(depth):
            parent = stack[-1]
            _, (_, left_right_depth) = parent
            left_right_depth[1] = depth
            return

       stack = [("go", (root, None))]

        while stack:
            go_back_flag, args = stack.pop()
            if go_back_flag == "go":
                node, direction = args
                if not node:
                    if not direction:
                        return 0
                    if direction == "left":
                        set_left_depth(0)
                    if direction == "right":
                        set_right_depth(0)
                    continue
                stack.append(("back", (direction, [None, None])))
                stack.append(("go", (node.right, "right")))
                stack.append(("go", (node.left, "left")))
            if go_back_flag == "back":
                direction, [left_depth, right_depth] = args
                if not direction:
                    return max(left_depth, right_depth) + 1
                if direction == "right":
                    right_depth = max(left_depth, right_depth) + 1
                    set_right_depth(right_depth)
                    continue
                if direction == "left":
                    left_depth = max(left_depth, right_depth) + 1
                    set_left_depth(left_depth)
                    continue
```