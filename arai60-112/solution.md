# 1st
- DFSで解いた
```py
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        def find_target_path_sum(node, path_sum):
            if not node:
                return False
            path_sum += node.val
            if not node.left and not node.right:
                return path_sum == targetSum
            return find_target_path_sum(node.left, path_sum) or find_target_path_sum(node.right, path_sum)
        return find_target_path_sum(root, 0)
```
- 再帰の引数ノードにNoneが含まれていないバージョン
```py
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        if not root:
            return False
        def find_target_sum(node, val):
            if not node.left and not node.right:
                return val == targetSum
            has_target_sum = False
            if node.left:
                has_target_sum |= find_target_sum(node.left, val + node.left.val)
            if node.right:
                has_target_sum |= find_target_sum(node.right, val + node.right.val)
            return has_target_sum
        return find_target_sum(root, root.val)
```
- スタックを用いた解法
- `if path_sum == targetSum:`じゃないときcontinueしてもよかった
```py
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        stack = [(root, 0)]
        while stack:
            node, path_sum = stack.pop()
            if not node:
                continue
            path_sum += node.val
            if not node.left and not node.right:
                if path_sum == targetSum:
                    return True
            stack.append((node.left, path_sum))
            stack.append((node.right, path_sum))
        return False
```
# 2nd
```py
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        def find_target_path_sum(node, val):
            if not node:
                return False
            val += node.val
            if not node.left and not node.right:
                return val == targetSum
            return find_target_path_sum(node.left, val) or find_target_path_sum(node.right, val)
        return find_target_path_sum(root, 0)
```
# 3rd
```py
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        def find_target_path_sum(node, val):
            if not node:
                return False
            new_val = val + node.val
            if not node.left and not node.right:
                return new_val == targetSum
            return find_target_path_sum(node.left, new_val) or find_target_path_sum(node.right, new_val)
        return find_target_path_sum(root, 0)
```