# 1st
- `range(2, posts + 1)`が不自然かもしれない
```py
class Solution:
    """
    @param n: non-negative integer, n posts
    @param k: non-negative integer, k colors
    @return: an integer, the total number of ways
    """
    def num_ways(self, n: int, k: int) -> int:
        # write your code here
        posts = n
        colors = k
        if posts == 0:
            return 0
        with_duplicate = 0
        without_duplicate = k
        for _ in range(2, posts + 1):
            tmp = with_duplicate
            with_duplicate = without_duplicate
            without_duplicate = tmp * (k - 1) + without_duplicate * (k - 1)
        return with_duplicate + without_duplicate
```
# 2nd 
- postsをincrementさせることでpostとwithout_duplicateやwith_duplicateの対応を分かりやすくした。
```py
class Solution:
    """
    @param n: non-negative integer, n posts
    @param k: non-negative integer, k colors
    @return: an integer, the total number of ways
    """
    def num_ways(self, n: int, k: int) -> int:
        # write your code here
        if n == 0:
            return 0
        posts = 1
        colors = k
        with_duplicate = 0
        without_duplicate = colors
        while posts < n:
            tmp = with_duplicate
            with_duplicate = without_duplicate
            without_duplicate = tmp * (colors - 1) + without_duplicate * (colors - 1)
            posts += 1
        return with_duplicate + without_duplicate
```

LRUCacheを用いた解法
```py
class Node:
    def __init__(self, key = None, val = None, next = None, prev = None):
        self.key = key
        self.val = val
        self.next = next
        self.prev = prev
class LRUCache:

    def __init__(self, capacity: int):
        self.capacity = capacity
        self.size = 0
        self.key_to_node = {}
        self.sentinel = Node(1, 1)
        self.sentinel.prev = self.sentinel
        self.sentinel.next = self.sentinel
        
    def get(self, key: int) -> int:
        if not key in self.key_to_node:
            return None
        node = self.key_to_node[key]
        self._remove(key)
        self._insert(key, node.val)
        return node.val    

    def put(self, key: int, value: int) -> None:
        if key in self.key_to_node:
            self._update(key, value)
            return
        self._insert(key, value)
        self.size += 1
        if self.size > self.capacity:
            least_node_key = self.sentinel.prev.key
            self._remove(least_node_key)
            self.size -= 1
    
    def _remove(self, key):
        node = self.key_to_node[key]
        del self.key_to_node[key]
        node.next.prev = node.prev
        node.prev.next = node.next
    
    def _insert(self, key, val):
        new_node = Node(key, val)
        self.key_to_node[key] = new_node
        next_node = self.sentinel.next
        next_node.prev = new_node
        self.sentinel.next = new_node
        new_node.prev = self.sentinel
        new_node.next = next_node
    
    def _update(self, key, val):
        self._remove(key)
        self._insert(key, val)

def my_lru_cache(maxsize = 100):
    def lru_cache_wrapper(func):
        cache = LRUCache(maxsize)
        def wrapped_func(*args, **kwargs):
            result = cache.get(args)
            if result:
                return result
            result = func(*args, **kwargs)
            cache.put(args, result)
            return result
        return wrapped_func
    return lru_cache_wrapper


class Solution:
    """
    @param n: non-negative integer, n posts
    @param k: non-negative integer, k colors
    @return: an integer, the total number of ways
    """
    @my_lru_cache(2000)
    def num_ways(self, n: int, k: int) -> int:
        if n == 2:
            return k * k
        if n == 1:
            return k
        else:
            return (k - 1) * self.num_ways(n -1, k) + (k - 1) * self.num_ways(n - 2, k)
```

# 3rd
- 2ndのtmpは変数名が良くないかもしれないので`with_duplicate_tmp`にした
- https://github.com/hayashi-ay/leetcode/pull/17/files
  - `with_duplicate`はどこかに重複があるというイメージで少し変数の中身と違うかもしれない`two_consective`とかのほうが良かった。
```py
class Solution:
    """
    @param n: non-negative integer, n posts
    @param k: non-negative integer, k colors
    @return: an integer, the total number of ways
    """
    def num_ways(self, n: int, k: int) -> int:
        if n == 0:
            return 0
        colors = k
        without_duplicate = colors
        with_duplicate = 0
        posts = 1
        while posts < n:
            with_duplicate_tmp = with_duplicate
            with_duplicate = without_duplicate
            without_duplicate = (colors - 1) * (without_duplicate + with_duplicate_tmp)
            posts += 1
        return without_duplicate + with_duplicate
```