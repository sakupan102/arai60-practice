# 1st
```py
class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> Optional[TreeNode]:
        if len(nums)  == 0:
            return None
        if len(nums) == 1:
            return TreeNode(nums[0], None, None)
        middle = len(nums) // 2 
        middle_val = nums[middle]
        left_tree = self.sortedArrayToBST(nums[:middle])
        right_tree = self.sortedArrayToBST(nums[middle + 1 :])
        return TreeNode(middle_val, left_tree, right_tree)
```
# 2nd
- https://github.com/hayashi-ay/leetcode/pull/29/files
  - left_right_flagをつけてstackを用いても解ける
```py
class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> Optional[TreeNode]:
        if len(nums) == 0:
            return None
        middle = len(nums) // 2
        node_val = nums[middle]
        left_tree = self.sortedArrayToBST(nums[:middle])
        right_tree = self.sortedArrayToBST(nums[middle + 1:])
        return TreeNode(node_val, left_tree, right_tree)
```
indexを引数にとってもいい
- 今回は閉区間だが閉開区間でとってもいい
```py
class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> Optional[TreeNode]:
        def createBST(start, end):
            if start > end:
                return None
            middle = (end + start) // 2
            node_val = nums[middle]
            left_tree = createBST(start, middle - 1)
            right_tree = createBST(middle + 1, end)
            return TreeNode(node_val, left_tree, right_tree)
        return createBST(0, len(nums) - 1)
```
# 3rd 
```py
class Solution:
    def sortedArrayToBST(self, nums: List[int]) -> Optional[TreeNode]:
        def createBST(start, end):
            if start > end:
                return None
            middle = (end + start) // 2
            node_val = nums[middle]
            left_tree = createBST(start, middle - 1)
            right_tree = createBST(middle + 1, end)
            return TreeNode(node_val, left_tree, right_tree)
        return createBST(0, len(nums) - 1)
```
