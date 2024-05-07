# 1st
```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root1 or not root2:
            return root1 or root2
        head_val = root1.val + root2.val
        left_tree = self.mergeTrees(root1.left, root2.left)
        right_tree = self.mergeTrees(root1.right, root2.right)
        return TreeNode(head_val, left_tree, right_tree)     
```

# 2nd
- https://github.com/hayashi-ay/leetcode/pull/12
  - 一方の木に足していくアプローチでも後で書く。
```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root1 or not root2:
            return root1 or root2
        left_tree = self.mergeTrees(root1.left, root2.left)
        right_tree = self.mergeTrees(root1.right, root2.right)
        node_val = root1.val + root2.val
        return TreeNode(node_val, left_tree, right_tree)
```

破壊的
```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root1 or not root2:
            return root1 or root2
        left_tree = self.mergeTrees(root1.left, root2.left)
        right_tree = self.mergeTrees(root1.right, root2.right)
        root1.val = root1.val + root2.val
        root1.right = right_tree
        root1.left = left_tree
        return root1
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
    def mergeTrees(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> Optional[TreeNode]:
        if not root1 or not root2:
            return root1 or root2
        left_tree = self.mergeTrees(root1.left, root2.left)
        right_tree = self.mergeTrees(root1.right, root2.right)
        node_val = root1.val + root2.val
        return TreeNode(node_val, left_tree, right_tree)
```