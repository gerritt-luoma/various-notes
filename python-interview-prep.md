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

### Doubly linked lists
- Linked lists where each node contains a pointer to the previous and next nodes in the chain