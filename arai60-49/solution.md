# 1st
```py
from collections import defaultdict
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        sorted_str_to_str_list = defaultdict(list)
        for string in strs:
            sorted_str = "".join(sorted(string))
            sorted_str_to_str_list[sorted_str].append(string)
        return sorted_str_to_str_list.values()
```