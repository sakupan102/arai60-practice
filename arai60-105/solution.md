# 1st
配列を引数にとる方法
```py
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        if not preorder:
            return None
        node_val = preorder[0]
        middle_index_inorder = inorder.index(node_val)
        middle_index_preorder = middle_index_inorder + 1
        left_tree = self.buildTree(preorder[1: middle_index_preorder], inorder[:middle_index_inorder])
        right_tree = self.buildTree(preorder[middle_index_preorder:], inorder[middle_index_inorder + 1:])
        return TreeNode(node_val, left_tree, right_tree)
```
# 2nd
- indexを引数にとる方法でやった
- https://github.com/hayashi-ay/leetcode/pull/43/files
  - 1stでは再帰ごとにO(n)かかるindexの探査がおこなわれる。
  - mapでindexを管理することで定数倍最適化しているのは参考になった。
  - `middle_index_inorder`はわかりずらいかもしれない。`num_left_nodes`とかに変えた方がいい
- https://github.com/Mike0121/LeetCode/pull/12/files
  - stackを用いた再帰でもかける
  - 親の右に付けるか左に付けるかをindexで判定しているのが参考になった
```py
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        val_to_inorder_index = {val: index for index, val in enumerate(inorder)}
        def build_tree_helper(pre_start, pre_end, in_start, in_end):
            if not pre_end > pre_start:
                return None
            node_val = preorder[pre_start]
            num_left_nodes = val_to_inorder_index[node_val] - in_start
            left_tree = build_tree_helper(pre_start + 1, pre_start + num_left_nodes + 1, in_start, in_start + num_left_nodes)
            right_tree = build_tree_helper(pre_start + num_left_nodes + 1, pre_end, in_start + num_left_nodes + 1, in_end)
            return TreeNode(node_val, left_tree, right_tree)
        return build_tree_helper(0, len(preorder), 0, len(inorder))
```
# 3rd
```py
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        val_to_inorder_index = {value: index for index, value in enumerate(inorder)}
        def build_tree_helper(pre_start, pre_end, in_start, in_end):
            if not pre_end > pre_start:
                return None
            node_val = preorder[pre_start]
            num_left_nodes = val_to_inorder_index[node_val] - in_start
            left_tree = build_tree_helper(pre_start + 1, pre_start + num_left_nodes + 1, in_start, in_start + num_left_nodes)
            right_tree = build_tree_helper(pre_start + num_left_nodes + 1, pre_end, in_start + num_left_nodes + 1, in_end)
            return TreeNode(node_val, left_tree, right_tree)
        return build_tree_helper(0, len(preorder), 0, len(inorder))
```
# stackを用いた解法
## 1st
- なんか読みずらい
- whileの外でwhileと同じような処理をしているので一緒にしたい
- in_start, in_endの範囲とparent_val_indexの位置関係でnodeを右に付けるか左に付けるか判定している。
- parent_val_indexだとinorderかpreorderか分からない
```py
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        val_to_inorder_index = {val: index for index, val in enumerate(inorder)}
        node_val = preorder[0]
        num_left_nodes = val_to_inorder_index[node_val]
        root  = TreeNode(node_val)
        stack = [(root, 1, num_left_nodes + 1, 0, num_left_nodes), (root, num_left_nodes + 1, len(preorder), num_left_nodes + 1, len(inorder))]
        while stack:
            parent, pre_start, pre_end, in_start, in_end = stack.pop()
            if not pre_end > pre_start:
                continue
            parent_val_index = val_to_inorder_index[parent.val]
            node_val = preorder[pre_start]
            num_left_nodes = val_to_inorder_index[node_val] - in_start
            next_node = TreeNode(node_val)
            stack.append((next_node, pre_start + 1, pre_start + num_left_nodes + 1, in_start, in_start + num_left_nodes))
            stack.append((next_node, pre_start + num_left_nodes + 1, pre_end, in_start + num_left_nodes + 1, in_end))
            if in_start > parent_val_index: #right
                parent.right = next_node
                continue
            else:
                parent.left = next_node
                continue
        return root
```
## 2nd
- https://github.com/Mike0121/LeetCode/pull/12/files
  - 子ノードの追加を次の再帰に任せるのではなく今の再帰でやってしまう方法
  - left_count, right_countで子ノードの追加を判定しているのが分かりやすい
```py
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        inorder_index_map = {value: index for index, value in enumerate(inorder)}
        root = TreeNode(preorder[0])
        stack = [(root, 0, len(preorder), 0, len(inorder))]
        while stack:
            node, pre_start, pre_end, in_start, in_end = stack.pop()
            inorder_mid = inorder_index_map[node.val]
            num_left_nodes = inorder_mid - in_start
            num_right_nodes = in_end - inorder_mid - 1
            if num_left_nodes > 0:
                left_node = TreeNode(preorder[pre_start + 1])
                node.left = left_node
                stack.append((left_node, pre_start + 1, pre_start + num_left_nodes + 1, in_start, inorder_mid))
            if num_right_nodes > 0:
                right_node = TreeNode(preorder[pre_end - num_right_nodes])
                node.right = right_node
                stack.append((right_node, pre_end - num_right_nodes, pre_end, inorder_mid + 1, in_end))
        return root
```