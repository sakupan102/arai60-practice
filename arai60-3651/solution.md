# 1st
```py
from collections import defaultdict
class Solution:
    """
    @param n: the number of vertices
    @param edges: the edges of undirected graph
    @return: the number of connected components
    """
    def count_components(self, n: int, edges: List[List[int]]) -> int:
        visited = [False] * n

        def make_adjacent_node_graph():
            node_to_adjacent_nodes = defaultdict(list)
            for edge in edges:
                node_to_adjacent_nodes[edge[0]].append(edge[1])
                node_to_adjacent_nodes[edge[1]].append(edge[0])
            return node_to_adjacent_nodes

        node_to_adjacent_nodes = make_adjacent_node_graph()

        def visit_connected_component(node):
            visited[node] = True
            for next_node in node_to_adjacent_nodes[node]:
                if not visited[next_node]:
                    visit_connected_component(next_node)

        num_connected_components = 0
        for node in range(n):
            if not visited[node]:
                num_connected_components += 1
                visit_connected_component(node)
        return num_connected_components
```
# 2nd
- https://github.com/hayashi-ay/leetcode/pull/37/files
  - 訪れているかの判定を次の再帰に任せてもよかった。
  - Union Findも使える
```py
from collections import defaultdict

class Solution:
    """
    @param n: the number of vertices
    @param edges: the edges of undirected graph
    @return: the number of connected components
    """
    def count_components(self, n: int, edges: List[List[int]]) -> int:
        num_nodes = n

        def make_adjacent_node_graph():
            node_to_adjacent_nodes = defaultdict(list)
            for node1, node2 in edges:
                node_to_adjacent_nodes[node1].append(node2)
                node_to_adjacent_nodes[node2].append(node1)
            return node_to_adjacent_nodes
        
        node_to_adjacent_nodes = make_adjacent_node_graph()
        visited = [False] * num_nodes
        def visit_connected_component(node):
            visited[node] = True
            for next_node in node_to_adjacent_nodes[node]:
                if not visited[next_node]:
                    visit_connected_component(next_node)

        num_connected_components = 0
        for node in range(num_nodes):
            if not visited[node]:
                num_connected_components += 1
                visit_connected_component(node)
        return num_connected_components
```

# 3rd
```py
from collections import defaultdict

class Solution:
    """
    @param n: the number of vertices
    @param edges: the edges of undirected graph
    @return: the number of connected components
    """
    def count_components(self, n: int, edges: List[List[int]]) -> int:
        num_nodes = n

        def make_adjacent_node_graph():
            node_to_adjacent_nodes = defaultdict(list)
            for node1, node2 in edges:
                node_to_adjacent_nodes[node1].append(node2)
                node_to_adjacent_nodes[node2].append(node1)
            return node_to_adjacent_nodes
        
        node_to_adjacent_nodes = make_adjacent_node_graph()
        visited = [False] * num_nodes

        def visit_connected_components(node):
            visited[node] = True
            for next_node in node_to_adjacent_nodes[node]:
                if not visited[next_node]:
                    visit_connected_components(next_node)
        
        num_connected_components = 0
        for node in range(num_nodes):
            if not visited[node]:
                num_connected_components += 1
                visit_connected_components(node)
        return num_connected_components
```