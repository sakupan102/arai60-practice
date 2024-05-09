# 1st
List2つを使った解法
```py
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        nodes = [root]
        level_order_node_vals = []
        while nodes:
            next_level_nodes = []
            node_vals = []
            for node in nodes:
                node_vals.append(node.val)
                if node.left:
                    next_level_nodes.append(node.left)
                if node.right:
                    next_level_nodes.append(node.right)
            nodes = next_level_nodes
            level_order_node_vals.append(node_vals)
        return level_order_node_vals
```
dequeを使った解法
- あまりよくない感じがする
- node_valsに値を入れていきdepthが変わった段階で`level_order_node_vals`に入れる
- 見るdepthは単調に増加していく(0 -> 0 -> 1 -> 0などは起こらない)ことを前提にこのコードを書いているが、見ている人には理解するのに時間がかかりそう
```py
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        next_nodes = deque()
        next_nodes.append((root, 0))
        level_order_node_vals = []
        current_depth = 0
        node_vals = []
        while next_nodes:
            node, depth = next_nodes.popleft()
            if node.left:
                next_nodes.append((node.left, depth + 1))
            if node.right:
                next_nodes.append((node.right, depth + 1))
            if depth == current_depth:
                node_vals.append(node.val)
                continue
            level_order_node_vals.append(node_vals)
            node_vals = [node.val]
            current_depth = depth
        level_order_node_vals.append(node_vals)
        return level_order_node_vals
```
# 2nd
- https://discord.com/channels/1084280443945353267/1200089668901937312/1211248049884499988
  - `len(level_order_node_vals)`今見ているdepthに満たない時に拡張を行う
  - 「depthに至るまでlevel_order_node_valsを拡張する」という意味を持たせるためにwhileを使った
```py
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        next_nodes = deque()
        next_nodes.append((root, 0))
        level_order_node_vals = [[]]
        while next_nodes:
            node, depth = next_nodes.popleft()
            while len(level_order_node_vals) <= depth:
                level_order_node_vals.append([])
            level_order_node_vals[depth].append(node.val)
            if node.left:
                next_nodes.append((node.left, depth + 1))
            if node.right:
                next_nodes.append((node.right, depth + 1))
        return level_order_node_vals
```
# 3rd
```py
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        nodes = [root]
        level_order_node_vals = []
        while nodes:
            next_level_nodes = []
            node_vals = []
            for node in nodes:
                node_vals.append(node.val)
                if node.left:
                    next_level_nodes.append(node.left)
                if node.right:
                    next_level_nodes.append(node.right)
            level_order_node_vals.append(node_vals)
            nodes = next_level_nodes
        return level_order_node_vals
```
