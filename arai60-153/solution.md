# 1st
- rotateしていたら`nums[i] > nums[i + 1]`になる部分があるのでそこを二分探査で探していく
- rotateしていなかった場合に違った処理をする必要があって少し面倒
```py
class Solution:
    def findMin(self, nums: List[int]) -> int:
        left = 0
        right = len(nums) - 1
        if nums[left] <= nums[right]:
            return nums[left]
        while right - left > 1:
            middle = (left + right) // 2
            if nums[left] < nums[middle]:
                left = middle
            else:
                right = middle
        return nums[right]
```
# 2nd
- https://github.com/Exzrgs/LeetCode/pull/11
  - 右端より大きい値で一番右側にあるものを探すと考えることもできる
  - こっちの方が1stよりも簡潔
閉区間
```py
class Solution:
    def findMin(self, nums: List[int]) -> int:
        left = 0
        right = len(nums) - 1
        while left < right:
            middle = (left + right) // 2
            if nums[middle] < nums[-1]:
                right = middle
            else:
                left = middle + 1
        return nums[left]
```
閉開区間
- こっちは境界を探すというニュアンスがありそう
```py
class Solution:
    def findMin(self, nums: List[int]) -> int:
        left = 0
        right = len(nums)
        while left < right:
            middle = (left + right) // 2
            if nums[middle] <= nums[-1]:
                right = middle
            else:
                left = middle + 1
        return nums[left]
```
# 3rd
```py
class Solution:
    def findMin(self, nums: List[int]) -> int:
        left = 0
        right = len(nums)
        while left < right:
            middle = (left + right) // 2
            if nums[middle] <= nums[-1]:
                right = middle
            else:
                left = middle + 1
        return nums[left]
```

