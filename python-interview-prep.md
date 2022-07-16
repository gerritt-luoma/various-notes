- [Python Interview Prep](#python-interview-prep)
  - [Linear Data Structures](#linear-data-structures)
    - [Singly linked lists](#singly-linked-lists)
      - [Swapping the value of two nodes in a singly linked list](#swapping-the-value-of-two-nodes-in-a-singly-linked-list)
    - [Doubly linked lists](#doubly-linked-lists)
    - [Linear search](#linear-search)
      - [Time complexity for Linear Search](#time-complexity-for-linear-search)
      - [Linear search with Python3 to find first occurrence](#linear-search-with-python3-to-find-first-occurrence)
      - [Linear search with Python3 to find **all** occurrences](#linear-search-with-python3-to-find-all-occurrences)
    - [Binary Search](#binary-search)
      - [Time complexity for binary search](#time-complexity-for-binary-search)
      - [Binary search with recursion](#binary-search-with-recursion)
      - [Binary search iterative approach](#binary-search-iterative-approach)
# Python Interview Prep
I am doing some interview prep using Codecademy's Python technical interview prep course.  These won't be robust notes but instead will be where I store all of the example code I write.

## Linear Data Structures

### Singly linked lists
- Linked lists where nodes only point to one other node

```
# Node class
# Contains a value and a pointer to the next node
class Node:
  def __init__(self, value, next_node=None):
    self.value = value
    self.next_node = next_node
    
  def get_value(self):
    return self.value
  
  def get_next_node(self):
    return self.next_node
  
  def set_next_node(self, next_node):
    self.next_node = next_node

# LinkedList class.  Contains a pointer to the head node
class LinkedList:
  def __init__(self, value=None):
    self.head_node = Node(value)
  
  def get_head_node(self):
    return self.head_node
  
  # A function to add a new node to the beginning of the LL
  # Did not implement a function to add a node to an index or specific location
  def insert_beginning(self, new_value):
    new_node = Node(new_value)
    new_node.set_next_node(self.head_node)
    self.head_node = new_node
    
  # Used to print out the entire linked list
  def stringify_list(self):
    string_list = ""
    current_node = self.get_head_node()
    while current_node:
      if current_node.get_value() != None:
        string_list += str(current_node.get_value()) + "\n"
      current_node = current_node.get_next_node()
    return string_list
  
  # Removes a node containing a specific value
  def remove_node(self, value_to_remove):
    current_node = self.get_head_node()
    if current_node.get_value() == value_to_remove:
      self.head_node = current_node.get_next_node()
    else:
      while current_node.get_next_node() != None:
        next_node = current_node.get_next_node()
        if next_node.get_value() == value_to_remove:
          current_node.set_next_node(next_node.get_next_node())
          break
        current_node = next_node
```

#### Swapping the value of two nodes in a singly linked list
- Given the input of 2 values (`val1`, `val2`) to find and swap in a **SINGLY** linked list you need to keep track of 4 items:
  1. `val1`
  2. The previous node of the node containing `val1`
  3. `val2`
  4. The previous node of the node containing `val2`
- Steps to swap:
  1. Iterate through the linked list keeping track of the `current_node` and the previous node calling it `node1_prev`.  Once you find the node containing `val1`, `node1_prev` will be the node before it.
  2. Repeat this process for `val2` calling the previous node `node2_prev`
  3. If the `node1_prev` is None, node1 was the head of the LL so set the head to `node2`
  4. Else, set `node1_prev`'s next node to node2
  5. If `node2_prev` is None, node2 was the head of the LL so set the head to `node2`
  6. Else, set `node2_prev`'s next node to node1

### Doubly linked lists
- Linked lists where each node contains a pointer to the previous and next nodes in the chain

```
class Node:
  def __init__(self, value, next_node=None, prev_node=None):
    self.value = value
    self.next_node = next_node
    self.prev_node = prev_node
    
  def set_next_node(self, next_node):
    self.next_node = next_node
    
  def get_next_node(self):
    return self.next_node

  def set_prev_node(self, prev_node):
    self.prev_node = prev_node
    
  def get_prev_node(self):
    return self.prev_node
  
  def get_value(self):
    return self.value


class DoublyLinkedList:
  def __init__(self):
    self.head_node = None
    self.tail_node = None
  
  def add_to_head(self, new_value):
    new_head = Node(new_value)
    current_head = self.head_node

    if current_head != None:
      current_head.set_prev_node(new_head)
      new_head.set_next_node(current_head)

    self.head_node = new_head

    if self.tail_node == None:
      self.tail_node = new_head

  def add_to_tail(self, new_value):
    new_tail = Node(new_value)
    current_tail = self.tail_node

    if current_tail != None:
      current_tail.set_next_node(new_tail)
      new_tail.set_prev_node(current_tail)

    self.tail_node = new_tail

    if self.head_node == None:
      self.head_node = new_tail

  def remove_head(self):
    removed_head = self.head_node

    if removed_head == None:
      return None

    self.head_node = removed_head.get_next_node()

    if self.head_node != None:
      self.head_node.set_prev_node(None)

    if removed_head == self.tail_node:
      self.remove_tail()

    return removed_head.get_value()

  def remove_tail(self):
    removed_tail = self.tail_node

    if removed_tail == None:
      return None

    self.tail_node = removed_tail.get_prev_node()

    if self.tail_node != None:
      self.tail_node.set_next_node(None)

    if removed_tail == self.head_node:
      self.remove_head()

    return removed_tail.get_value()

  def remove_by_value(self, value_to_remove):
    node_to_remove = None
    current_node = self.head_node

    while current_node != None:
      if current_node.get_value() == value_to_remove:
        node_to_remove = current_node
        break

      current_node = current_node.get_next_node()

    if node_to_remove == None:
      return None

    if node_to_remove == self.head_node:
      self.remove_head()
    elif node_to_remove == self.tail_node:
      self.remove_tail()
    else:
      next_node = node_to_remove.get_next_node()
      prev_node = node_to_remove.get_prev_node()
      next_node.set_prev_node(prev_node)
      prev_node.set_next_node(next_node)

    return node_to_remove

  def stringify_list(self):
    string_list = ""
    current_node = self.head_node
    while current_node:
      if current_node.get_value() != None:
        string_list += str(current_node.get_value()) + "\n"
      current_node = current_node.get_next_node()
    return string_list
```

### Linear search
- Linear search is a search algorithm that starts at the beginning of a linear data structure and scans each item one by one until it finds the desired item.  Linear search doesn't need to be used on a sorted structure since it scans each item.
- Linear search is great for small datasets or if you expect a target to be near the beginning of the set but it is not idea for larger structures.

#### Time complexity for Linear Search
| Case | Value |
| ---- | ----- |
| Worst| O(N)  |
| Best | O(1)  |
| Average | O(N/2) |

#### Linear search with Python3 to find first occurrence
```
def linear_search(search_list, target_value):
  for i, value in enumerate(search_list):
    if value == target_value:
      return i
  raise ValueError(f"{target_value} not in list")
```
#### Linear search with Python3 to find **all** occurrences
```
def linear_search(search_list, target_value):
  matches = []
  for i, value in enumerate(search_list):
    if value == target_value:
      matches.append(i)
  if matches:
    return matches
  raise ValueError(f"{target_value} not in list")
```

### Binary Search
- Binary search is a much more efficient search algorithm that requires the list/array to be sorted prior to searching.  The idea of binary search is that you start in the middle of the structure, check if the middle value is less or greater tahn the target value, and then checking top or bottom half depending on the check

#### Time complexity for binary search
| Case | Value |
| ---- | ----- |
| Worst| O(log(n))  |
| Best | O(1)  |
| Average | O(log(n)) |

#### Binary search with recursion
```
def binary_search(sorted_list, left_pointer, right_pointer, target):
  if left_pointer >= right_pointer:
    return "value not found"
	
  mid_idx = (left_pointer + right_pointer) // 2
  mid_val = sorted_list[mid_idx]

  if mid_val == target:
    return mid_idx
  
  if mid_val > target:
    return binary_search(sorted_list, left_pointer, mid_idx, target)
  
  if mid_val < target:
    return binary_search(sorted_list, mid_idx + 1, right_pointer, target)
```

#### Binary search iterative approach
```
def binary_search(sorted_list, target):
  left_pointer = 0
  right_pointer = len(sorted_list)
  
  while left_pointer < right_pointer:
    mid_idx = (left_pointer + right_pointer) // 2
    mid_val = sorted_list[mid_idx]
    
    if mid_val == target:
      return mid_idx
    
    if target < mid_val:
      right_pointer = mid_idx
    
    if target > mid_val:
      left_pointer = mid_idx + 1
  
  return "Value not in list"
```