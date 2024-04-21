# 1st
```py
import heapq
class Solution:
    def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) -> List[List[int]]:
        min_num_pair = []
        k_smallest_pair = []
        for num1 in nums1:
            heapq.heappush(min_num_pair, (num1 + nums2[0], 0))
        for _ in range(k):
            added_val, nums2_index = heapq.heappop(min_num_pair)
            num2 = nums2[nums2_index]
            num1 = added_val - num2
            k_smallest_pair.append([num1, num2])
            if not nums2_index + 1 < len(nums2):
                continue
            new_index = nums2_index + 1
            heapq.heappush(min_num_pair, (num1 + nums2[new_index], new_index))
        return k_smallest_pair
```
# 2nd
```py
import heapq
class Solution:
    def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) -> List[List[int]]:
        def able_to_add(index1, index2):
            if not (index1 < len(nums1) and index2 < len(nums2)):
                return False
            if index1 == 0 or index2 == 0:
                return True
            return (index1 - 1, index2) in added and (index1, index2 - 1) in added
        min_num_pairs = []
        added = set()
        candidate = [(nums1[0] + nums2[0], 0, 0)]
        for _ in range(k):
            _, index1, index2 = heapq.heappop(candidate)
            min_num_pairs.append([nums1[index1], nums2[index2]])
            added.add((index1, index2))
            if able_to_add(index1 + 1, index2):
                heapq.heappush(candidate, (nums1[index1 + 1] + nums2[index2], index1 + 1, index2))
            if able_to_add(index1, index2 + 1):
                heapq.heappush(candidate, (nums1[index1] + nums2[index2 + 1], index1, index2 + 1))
        return min_num_pairs
```
# 3rd