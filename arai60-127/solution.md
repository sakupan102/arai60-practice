# 1st
- 最初に隣接リストを作ってBFSをする
```py
from collections import deque, defaultdict
class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        wordList.append(beginWord)

        def create_word_graph(wordList):
            connected = defaultdict(set)
            for index1 in range(len(wordList) - 1):
                for index2 in range(index1 + 1, len(wordList)):
                    num_different_char = 0
                    word1 = wordList[index1]
                    word2 = wordList[index2]
                    for i in range(len(word1)):
                        if num_different_char > 1:
                            break
                        if word1[i] != word2[i]:
                            num_different_char += 1
                    if num_different_char == 1:
                        connected[index1].add(index2)
                        connected[index2].add(index1)
            return connected
        
        def find_shortest_path(connected_word_graph):
            visited = [False] * len(wordList)
            next_visit = deque()
            next_visit.append((len(wordList) - 1, 1))
            visited[len(wordList) - 1] = True
            while next_visit:
                current_index, path = next_visit.popleft()
                if wordList[current_index] == endWord:
                    return path
                for next_index in connected_word_graph[current_index]:
                    if not visited[next_index]:
                        next_visit.append((next_index, path + 1))
                        visited[next_index] = True
            return 0
        
        connected_word_graph = create_word_graph(wordList)
        
        return find_shortest_path(connected_word_graph)
```

# 2nd
- https://github.com/hayashi-ay/leetcode/pull/42/files
  - 探索しているときにwordが隣り合っているかの判定をしてもいいが時間がかかりそう
  - find_shortest_pathは関数化しなくてもいいかも
- 1stでは隣接リストをsetで管理していたがhashや衝突などにかかる処理を考えて2ndではデータ構造として単純なlistを用いた。
- DFSでかんりするdequeはnext_visit_and_pathではなく`cells_to_visit_and_path`にした方が良かった
```py
from collections import deque, defaultdict
class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        wordList.append(beginWord)

        def adjacent_word(word1, word2):
            different_char_count = 0
            for i in range(len(word1)):
                if different_char_count > 1:
                    return False
                if word1[i] != word2[i]:
                    different_char_count += 1
            return different_char_count == 1


        def create_word_graph(wordList):
            adjacent_index = defaultdict(list)
            word_list_length = len(wordList)
            for index1 in range(word_list_length - 1):
                for index2 in range(index1 + 1, word_list_length):
                    if adjacent_word(wordList[index1], wordList[index2]):
                        adjacent_index[index1].append(index2)
                        adjacent_index[index2].append(index1)
            return adjacent_index
        
        def find_shortest_path(adjacent_index):
            visited = [False] * len(wordList)
            visited[-1] = True
            next_visit_and_path = deque([(len(wordList) - 1, 1)])
            while next_visit_and_path:
                current_index, path = next_visit_and_path.popleft()
                if wordList[current_index] == endWord:
                    return path
                for next_index in adjacent_index[current_index]:
                    if not visited[next_index]:
                        visited[next_index] = True
                        next_visit_and_path.append((next_index, path + 1))
            return 0

        adjacent_index = create_word_graph(wordList)
        return find_shortest_path(adjacent_index)
```

# 3rd
```py
from collections import deque, defaultdict
class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        wordList.append(beginWord)

        def adjacent_word(word1, word2):
            different_char_count = 0
            for i in range(len(word1)):
                if different_char_count > 1:
                    return False
                if word1[i] != word2[i]:
                    different_char_count += 1
            return different_char_count == 1


        def create_adjacent_word_list(wordList):
            adjacent_word_indexes = defaultdict(list)
            for index1 in range(len(wordList) - 1):
                for index2 in range(index1 + 1, len(wordList)):
                    if adjacent_word(wordList[index1], wordList[index2]):
                        adjacent_word_indexes[index1].append(index2)
                        adjacent_word_indexes[index2].append(index1)
            return adjacent_word_indexes

        adjacent_word_indexes = create_adjacent_word_list(wordList)
        visited = [False] * len(wordList)
        cells_to_visit_and_path = deque([(len(wordList) - 1, 1)])
        visited[-1] = True
        while cells_to_visit_and_path:
            current_index, path = cells_to_visit_and_path.popleft()
            if wordList[current_index] == endWord:
                return path
            for next_index in adjacent_word_indexes[current_index]:
                if not visited[next_index]:
                    visited[next_index] = True
                    cells_to_visit_and_path.append((next_index, path + 1)) 
        return 0
        
```
# TLEした解答
- wordどうしが隣り合っているかどうか判定する箇所で時間がかかったと推測
- distance(word1, word2) = distance(word2, word1)なので一つにまとめたい。
```py
from collections import deque, defaultdict
class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        wordList.append(beginWord)

        def create_word_graph(wordList):
            connected = defaultdict(set)
            for index1, word1 in enumerate(wordList):
                for index2, word2 in enumerate(wordList):
                    num_different_char = 0
                    for i in range(len(word1)):
                        if num_different_char > 1:
                            break
                        if word1[i] != word2[i]:
                            num_different_char += 1
                    if num_different_char == 1:
                        connected[index1].add(index2)
                        connected[index2].add(index1)
            return connected
        
        def find_shortest_path(connected_word_graph):
            visited = [False] * len(wordList)
            next_visit = deque()
            next_visit.append((len(wordList) - 1, 1))
            visited[len(wordList) - 1] = True
            while next_visit:
                current_index, path = next_visit.popleft()
                if wordList[current_index] == endWord:
                    return path
                for next_index in connected_word_graph[current_index]:
                    if not visited[next_index]:
                        next_visit.append((next_index, path + 1))
                        visited[next_index] = True
            return 0
        
        connected_word_graph = create_word_graph(wordList)
        
        return find_shortest_path(connected_word_graph)
```