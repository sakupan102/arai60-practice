# 1st 
- rotateの回数を調べてその分だけずれた二分探索を行う
- 最初は閉区間でとってるのに二番目の二分探索は半開区間でとってるのが違和感
- `(left + rotate) % len(nums)`は変数名を付けた方がよさそう
```py
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums)
        while left < right:
            middle = (left + right) // 2
            if nums[middle] <= nums[-1]:
                right = middle
            else:
                left = middle + 1

        rotate = left
        left = 0
        right = len(nums) - 1

        while left < right:
            middle = (left + right) // 2
            rotated_middle = (middle + rotate) % len(nums)
            if nums[rotated_middle] == target:
                return rotated_middle
            if nums[rotated_middle] < target:
                left = middle + 1
            else:
                right = middle
        
        if nums[(left + rotate) % len(nums)] == target:
            return (left + rotate) % len(nums)
        else:
            return -1
```
# 2nd
- https://github.com/hayashi-ay/leetcode/pull/49/files
  - pivotを見つける処理とtargetを見つける処理をそれぞれ関数化した方が良いかもしれない
  - nums[i]とnums[-1]を比較してnums[i]の方が大きい場合は左側は昇順に並んでいる。それ以外の場合は右側が昇順に並んでいる。
targetが昇順に並んでいる側の範囲にあればそちらを見に行く。そうでなければ反対側を見に行く。
      - これなら二分探索は1回で済む
  - pivot_indexによってtargetが右にあるか左にあるか決まる

二分探索を二回行った解法
- https://github.com/shining-ai/leetcode/pull/43/files
  - find_pivotの引数は無くてもよかったかも
```py
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        def find_pivot(nums):
            left = 0
            right = len(nums)
            while left < right:
                middle = (left + right) // 2
                if nums[middle] > nums[-1]:
                    left = middle + 1
                else:
                    right = middle  
            return left
        
        def binary_search(left, right):
            while left <= right:
                middle = (left + right) // 2
                if nums[middle] == target:
                    return middle
                if nums[middle] > target:
                    right = middle - 1
                else:
                    left = middle + 1
            return -1
        
        pivot_index = find_pivot(nums)
        if nums[pivot_index] <= target <= nums[-1]:
            return binary_search(pivot_index, len(nums) - 1)
        elif nums[0] <= target <= nums[pivot_index - 1]:
            return binary_search(0, pivot_index)
        return -1
```

二分探索1回のみの解法
```py
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0 
        right = len(nums) - 1
        while left <= right:
            middle = (left + right) // 2
            if nums[middle] == target:
                return middle
            if nums[middle] > nums[-1]:
                if nums[0] <= target < nums[middle]:
                    right = middle - 1
                else:
                    left = middle + 1
            elif nums[middle] < nums[-1]:
                if nums[middle] < target <= nums[-1]:
                    left = middle + 1
                else:
                    right = middle - 1
        return  -1
```
# 3rd 
```py
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        while left <= right:
            middle = (left + right) // 2
            if nums[middle] == target:
                return middle
            if nums[middle] > nums[-1]: #middleより左側は単調増加
                if nums[0] <= target < nums[middle]:
                    right = middle - 1
                else:
                    left = middle + 1
            else: #middleより右側は単調増加
                if nums[middle] < target <= nums[-1]:
                    left = middle + 1
                else:
                    right = middle - 1
        return -1
```

