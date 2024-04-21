# 1st
- 最小の和をもつ候補をmin_num_pairに入れていく
- `nums1[i] + nums[j]`がポップされたら次の最小値の候補`nums1[i] + nums[j + 1]`を入れる
- k_smallest_num_pairは二回目のfor文の直前に置いた方がよかった。
- min_num_pairはminimum_num_pairにしてもよかったかも
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
- https://discord.com/channels/1084280443945353267/1183683738635346001/1187326805015810089
  - これを参考にアルゴリズムを変更
- https://discord.com/channels/1084280443945353267/1200089668901937312/1222573940610695341
  - > あと、本当は、(x - 1, y) と (x, y - 1) が両方 pairs の中にある、または、x, y どちらかが0でなければ、heap に足さなくていいとは思うんですよね。
    - 例えば(x - 1, y)がpairsで(x, y - 1)がpairsに入ってないとき、(x, y - 1)はcandidateに入っている
    - (x, y- 1)の値の方が(x, y)の値より小さいのでcandidateに入れる必要がない
- addedはable_to_addで使うので一番上で定義した方がよかった。
- >今回の問題では、すべての情報が来たあとに、ソートをするという方法で、Top K Frequency を出すのではなく、常に Top K Frequency をモニタリングし続けるというストリーミングアルゴリズムとして解くことも可能ではないかという話です。具体的にはカウントを大きい順に並べた平衡木を用意しておけば、よさそうです。
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
```py
import heapq
class Solution:
    def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) -> List[List[int]]:
        added = set()
        def need_to_add(index1, index2):
            if not (index1 < len(nums1) and index2 < len(nums2)):
                return False
            if index1 == 0 or index2 == 0:
                return True
            return (index1 - 1, index2) in added and (index1, index2 - 1) in added
        minimum_num_pairs = []
        candidates = []
        heapq.heappush(candidates, (nums1[0] + nums2[0], 0, 0))
        for _ in range(k):
            _, index1, index2 = heapq.heappop(candidates)
            added.add((index1, index2))
            minimum_num_pairs.append([nums1[index1], nums2[index2]])
            if need_to_add(index1 + 1, index2):
                heapq.heappush(candidates, (nums1[index1 + 1] + nums2[index2], index1 + 1, index2))
            if need_to_add(index1, index2 + 1):
                heapq.heappush(candidates, (nums1[index1] + nums2[index2 + 1], index1, index2 + 1))
        return minimum_num_pairs
```