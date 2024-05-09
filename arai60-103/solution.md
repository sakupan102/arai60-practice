# 1st
- zigzag_ordered_node_valsにするべきだった
- nodesではなくsame_level_nodesにした方が良かった
```py
class Solution:
    def zigzagLevelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        zigzag_order_node_vals = []
        depth = 1
        nodes = [root]
        while nodes:
            next_level_nodes = []
            node_vals = []
            for node in nodes:
                node_vals.append(node.val)
                if node.left:
                    next_level_nodes.append(node.left)
                if node.right:
                    next_level_nodes.append(node.right)
            if depth % 2 == 0:
                node_vals.reverse()        
            zigzag_order_node_vals.append(node_vals)
            nodes = next_level_nodes
            depth += 1
        return zigzag_order_node_vals
```

# 2nd
- dequeを用いて`node_vals`をreverseする処理を無くした
- https://github.com/Mike0121/LeetCode/pull/10#discussion_r1590301468
  - nodeかnode_valの順番を固定しないと処理がふえてしまう
  
```py
from collections import deque
class Solution:
    def zigzagLevelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        zigzag_order_node_vals = []
        nodes = [root]
        depth = 0
        while nodes:
            next_level_nodes = []
            node_vals = deque()
            for node in nodes:
                if node.left:
                    next_level_nodes.append(node.left)
                if node.right:
                    next_level_nodes.append(node.right)
                if depth % 2 == 1:
                    node_vals.appendleft(node.val)
                else:
                    node_vals.append(node.val)
            depth += 1
            zigzag_order_node_vals.append(node_vals)
            nodes = next_level_nodes
        return zigzag_order_node_vals
```
# 3rd
```py
from collections import deque
class Solution:
    def zigzagLevelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return []
        zigzag_order_node_vals = []
        nodes = [root]
        depth = 0
        while nodes:
            next_level_nodes = []
            node_vals = deque()
            for node in nodes:
                if node.left:
                    next_level_nodes.append(node.left)
                if node.right:
                    next_level_nodes.append(node.right)
                if depth % 2 == 1:
                    node_vals.appendleft(node.val)
                else:
                    node_vals.append(node.val)
            zigzag_order_node_vals.append(node_vals)
            nodes = next_level_nodes
            depth += 1
        return zigzag_order_node_vals
```