- ヒープの中身をheap_bodyとして中身で定義したが、クラスmy_heapはheaに関する関数群として定義した方がよかったかも
```python
class my_heap:
  def __init__(self, ar0ay):
    self.heap_body = array
    self.heapify()

  def heap_push(self, val):
    self.heap_body.append(val)
    current = len(self.heap_body) - 1
    parent = self._parent(current)
    while current > 0 and self.heap_body[current] < self.heap_body[parent]:
      self._swap(current, parent)
      current = parent
      parent = self._parent(current)

  def heap_pop(self):
    self._swap(0, len(self.heap_body) - 1)
    self.heap_body.pop()
    self._partial_heapify(0)

  def heapify(self):
    for i in range(len(self.heap_body) - 1, -1, -1):
      self._partial_heapify(i)

  def _partial_heapify(self, index):
    if not self._has_child(index):
      return 
    min_child_index = self._min_child(index)
    if self.heap_body[index] <= self.heap_body[min_child_index]:
      return
    self._swap(index, min_child_index)
    self._partial_heapify(min_child_index)

  def _parent(self, index):
    return (index - 1) // 2

  def _left_child(self, index):
    return index * 2 + 1
  
  def _right_child(self, index):
    return index * 2 + 2

  def _has_parent(self, index):
    if self._parent(index) < 0:
      return False
    else:
      return True
  
  def _has_right_child(self, index):
    child_index = self._right_child(index)
    if child_index >= len(self.heap_body):
      return False
    else:
      return True

  def _has_left_child(self, index):
    child_index = self._left_child(index)
    if child_index >= len(self.heap_body):
      return False
    else:
      return True

  def _has_child(self, index):
    return self._has_left_child(index)

  def _min_child(self, index):
    if not self._has_right_child(index):
      return self._left_child(index)
    right_child = self._right_child(index)
    left_child = self._left_child(index)
    if self.heap_body[right_child] < self.heap_body[left_child]:
      return right_child
    return left_child
  
  def _swap(self, index1, index2):
    tmp = self.heap_body[index1]
    self.heap_body[index1] = self.heap_body[index2]
    self.heap_body[index2] = tmp
  

data = [5, 4, 6, -3, 3, 10, 2, 0]
new_heap = my_heap(data)
print(new_heap.heap_body) #[-3, 0, 2, 4, 3, 10, 6, 5]
new_heap.heap_push(-4)
print(new_heap.heap_body) #[-4, -3, 2, 0, 3, 10, 6, 5, 4]
new_heap.heap_pop()
print(new_heap.heap_body) #[-3, 0, 2, 4, 3, 10, 6, 5]
```