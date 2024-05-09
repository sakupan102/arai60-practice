# 1st
下からvalidateする方法
関数`validate_BST_helper`は(validBSTかどうか, 木の最小値, 木の最大値)を返す
```py
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        def validate_BST_helper(node):
            inf = float("inf")
            if not node.left and not node.right: # return (is_valid, min_val, max_val)
                return (True, node.val, node.val)
            left_val = node.val
            right_val = node.val
            max_val_left = -inf
            min_val_right = inf
            if node.left:
                is_valid_left_tree, left_val, max_val_left = validate_BST_helper(node.left)
                if not is_valid_left_tree:
                    return (False, -inf, inf)
            if node.right:
                is_valid_right_tree, min_val_right, right_val = validate_BST_helper(node.right)
                if not is_valid_right_tree:
                    return (False, -inf, inf)
            if not (max_val_left < node.val < min_val_right):
                return (False, -inf, inf)
            return (True, left_val, right_val)
        
        return validate_BST_helper(root)[0]
```
上からvalidateする方法
```py
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        inf = float("inf")
        stack = [(root, -inf, inf)]
        while stack:
            node, left_val, right_val = stack.pop()
            if not node:
                continue
            if not (left_val < node.val < right_val):
                return False
            stack.append((node.left, left_val, node.val))
            stack.append((node.right, node.val, right_val))
        return True
```
上からvalidateする方法(再帰バージョン)
```py
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        inf = float("inf")
        def is_valid_BST_helper(node, left_val, right_val):
            if not node:
                return True
            if not (left_val < node.val < right_val):
                return False
            is_valid_BST_left = is_valid_BST_helper(node.left, left_val, node.val)
            is_valid_BST_right = is_valid_BST_helper(node.right, node.val, right_val)
            return is_valid_BST_left and is_valid_BST_right
        return is_valid_BST_helper(root, -inf, inf)
```
inorderでたどる方法
```py
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        def convert_BST_to_inorder_list(node):
            if not node:
                return []
            middle_val = node.val
            left_array = convert_BST_to_inorder_list(node.left)
            right_array = convert_BST_to_inorder_list(node.right)
            return left_array + [middle_val] + right_array
        inorder_array = convert_BST_to_inorder_list(root)
        for i in range(len(inorder_array) - 1):
            if not inorder_array[i + 1] > inorder_array[i]:
                return False
        return True
```

# 2nd
- https://github.com/Mike0121/LeetCode/pull/8
  - 1stではinorderのリストをつくって判定していたが、inorderでstackに入れながらvalid BSTかどうか判定すれば計算時間は減る
```py
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        nodes = []
        inf = float("inf")
        def push_left_tree(node):
            while node:
                nodes.append(node)
                node = node.left
        push_left_tree(root)
        prev_val = -inf
        while nodes:
            node = nodes.pop()
            if prev_val >= node.val:
                return False
            if node.right:
                push_left_tree(node.right)
            prev_val = node.val
        return True
```

# 3rd
```py
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        node_stack = []

        def append_left_nodes(node):
            while node:
                node_stack.append(node)
                node = node.left
        
        prev_val = -float("inf")
        append_left_nodes(root)
        while node_stack: 
            node = node_stack.pop()
            if prev_val >= node.val:
                return False
            if node.right:
                append_left_nodes(node.right)
            prev_val = node.val
        return True
```
