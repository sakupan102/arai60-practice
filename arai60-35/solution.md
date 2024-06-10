# 1st
- target以上で一番左側にある番号のindexを返すという考え方でやった
- target以上のnumが無い場合、特別な処理をしてあげる必要がある
```py
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        while left < right:
            middle = (left + right) // 2
            if nums[middle] == target:
                return middle
            if target < nums[middle]:
                right = middle
            else:
                left = middle + 1
        if nums[left] < target:
            return left + 1
        return left
```
# 2nd 
- target以上のものと未満のものを分ける境界線を探す問題ととらえることもできる
- こちらの方が1stのやつより簡潔
- https://github.com/python/cpython/blob/main/Lib/bisect.py#L74
  - bisectの実装では閉開区間を使ってた
```py
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums)
        while left < right:
            middle = (left + right) // 2
            if nums[middle] >= target:
                right = middle
            else:
                left = middle + 1
        return left
```
# 3rd
```py
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums)
        while left < right:
            middle = (right + left) // 2
            if target > nums[middle]:
                left = middle + 1
            else:
                right = middle
        return left
        
```