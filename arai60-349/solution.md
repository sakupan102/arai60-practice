# 1st
-　intersectionに入れる処理は`list(nums1_set & nums2_set)`でもできる
```py
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        num_set1 = set()
        num_set2 = set()
        for num1 in nums1:
            num_set1.add(num1)
        for num2 in nums2:
            num_set2.add(num2)
        intersection = []
        for num1 in num_set1:
            if num1 in num_set2:
                intersection.append(num1)
        return intersection
```
# 2nd 
- https://github.com/shining-ai/leetcode/pull/13/files
  - これを参考に線形時間で解ける解法に変更
- `nums1.sort()`は副作用があるので`sorted_nums1 = nums1.sorted()`とかにした方がよかったかも
  - 空間計算量が増えるのでメモリに不安がある場合は`nums1.sort`でもよい
```py
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        nums1.sort()
        nums2.sort()
        index1, index2 = 0, 0
        intersection = []
        while index1 < len(nums1) and index2 < len(nums2):
            if nums1[index1] < nums2[index2]:
                index1 += 1
                continue
            if nums1[index1] > nums2[index2]:
                index2 += 1
                continue
            intersection.append(nums1[index1])
            while index1 < len(nums1) and nums1[index1] == nums2[index2]:
                index1 += 1
        return intersection
```
# 3rd
```py
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        sorted_nums1 = sorted(nums1)
        sorted_nums2 = sorted(nums2)
        index1, index2 = 0, 0
        intersection = []
        while index1 < len(sorted_nums1) and index2 < len(sorted_nums2):
            if sorted_nums1[index1] < sorted_nums2[index2]:
                index1 += 1
                continue
            if sorted_nums1[index1] > sorted_nums2[index2]:
                index2 += 1
                continue
            intersection.append(sorted_nums1[index1])
            while index1 < len(sorted_nums1) and sorted_nums1[index1] == sorted_nums2[index2]:
                index1 += 1
        return intersection
```
# 4th
```py
from collections import defaultdict
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        nums1_set = set(nums1)
        nums2_set = set(nums2)
        return list(nums1_set & nums2_set)
```