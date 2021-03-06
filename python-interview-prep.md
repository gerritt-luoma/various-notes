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
    - [Queues](#queues)
      - [Queue code example](#queue-code-example)
    - [Stacks](#stacks)
      - [Stack code example](#stack-code-example)
      - [Stack towers of Hanoi](#stack-towers-of-hanoi)
  - [Hash Maps](#hash-maps)
    - [Hash Functions](#hash-functions)
    - [Collisions](#collisions)
    - [Hash map code example using open addressing](#hash-map-code-example-using-open-addressing)
  - [Algorithms](#algorithms)
    - [Recursion](#recursion)
      - [Pseudocode example](#pseudocode-example)
      - [The Base Case and Recursive Step](#the-base-case-and-recursive-step)
    - [Algorithmic Complexity (Big-O)](#algorithmic-complexity-big-o)
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

### Queues
- Queues are a data structure with a first in first out (`FIFO`) approach similar to when you get in a line at an amusement park.
- For queues all you need to keep track of is the front and last so you can enqueue and dequeue the head/tail
- You can also put a length constraint on the queue to turn it to a "bounded queue"
  
#### Queue code example
```
class Node:
  def __init__(self, value, next_node=None):
    self.value = value
    self.next_node = next_node
    
  def set_next_node(self, next_node):
    self.next_node = next_node
    
  def get_next_node(self):
    return self.next_node
  
  def get_value(self):
    return self.value

class Queue:
  def __init__(self, max_size=None):
    self.head = None
    self.tail = None
    self.max_size = max_size
    self.size = 0
    
  def enqueue(self, value):
    if self.has_space():
      item_to_add = Node(value)
      print("Adding " + str(item_to_add.get_value()) + " to the queue!")
      if self.is_empty():
        self.head = item_to_add
        self.tail = item_to_add
      else:
        self.tail.set_next_node(item_to_add)
        self.tail = item_to_add
      self.size += 1
    else:
      print("Sorry, no more room!")
      
  # Add your dequeue method below:    
  def dequeue(self):
    if not self.is_empty():
      item_to_remove = self.head
      print("Removing " + str(item_to_remove.get_value()) + " from the queue!")
      if self.get_size() == 1:
        self.head = None
        self.tail = None
      else:
        self.head = item_to_remove.get_next_node()
      self.size -= 1
      return item_to_remove.get_value()
    print("This queue is totally empty!")
  
  def peek(self):
    if self.is_empty():
      print("Nothing to see here!")
    else:
      return self.head.get_value()
  
  def get_size(self):
    return self.size
  
  def has_space(self):
    if self.max_size == None:
      return True
    else:
      return self.max_size > self.get_size()
    
  def is_empty(self):
    return self.size == 0
```

### Stacks
- Stacks are a similar structure to queues but instead of following the `FIFO` approach they use first in last out, `FILO` (like in RotSH)
- Imagine like putting plates into the sink to clean.  The first one put in will be the last one out of the sink when being cleaned

#### Stack code example
```
class Node:
  def __init__(self, value, next_node=None):
    self.value = value
    self.next_node = next_node
    
  def set_next_node(self, next_node):
    self.next_node = next_node
    
  def get_next_node(self):
    return self.next_node
  
  def get_value(self):
    return self.value

class Stack:
  def __init__(self, limit=1000):
    self.top_item = None
    self.size = 0
    self.limit = limit
  
  def push(self, value):
    if self.has_space():
      item = Node(value)
      item.set_next_node(self.top_item)
      self.top_item = item
      self.size += 1
      print("Adding {} to the stack!".format(value))
    else:
      print("No room for {}!".format(value))

  def pop(self):
    if not self.is_empty():
      item_to_remove = self.top_item
      self.top_item = item_to_remove.get_next_node()
      self.size -= 1
      print("Popping " + item_to_remove.get_value())
      return item_to_remove.get_value()
    print("Stack is empty.")

  def peek(self):
    if not self.is_empty():
      return self.top_item.get_value()
    print("Stack is empty!")

  def has_space(self):
    return self.limit > self.size

  def is_empty(self):
    return self.size == 0
```

#### Stack towers of Hanoi
```
from stack import Stack

print("\nLet's play Towers of Hanoi!!")

#Create the Stacks
stacks = []
left_stack = Stack("Left")
middle_stack = Stack("Middle")
right_stack = Stack("Right")
stacks.append(left_stack)
stacks.append(middle_stack)
stacks.append(right_stack)

#Set up the Game
num_discs = int(input("\nHow many disks do you want to play with?\n"))
while num_discs < 3:
  num_discs = int(input("Enter a number greater than or equal to 3\n"))

for i in range(num_discs, 0, -1):
  left_stack.push(i)

num_optimal_moves = 2**num_discs - 1
print("\nThe fastest you can solve this game is in {0} moves".format(num_optimal_moves))
#Get User Input
def get_input():
  choices = [stack.get_name()[0] for stack in stacks]
  while True:
    for i in range(len(stacks)):
      name = stacks[i].get_name()
      letter = choices[i]
      print(f"Enter {letter} for {name}")
    user_input = input("")
    if user_input in choices:
      for i, stack in enumerate(stacks):
        if user_input == choices[i]:
          return stack
        
#Play the Game
num_user_moves = 0
while right_stack.get_size() != num_discs:
  print("\n\n\n...Current Stacks...")
  for stack in stacks:
    print(stack.print_items())
  while True:
    print("\nWhich stack do you want to move from?\n")
    from_stack = get_input()
    print("\nWhich stack do you want to move to?\n")
    to_stack = get_input()
    if from_stack.is_empty():
      print("\n\nInvalid Move. Try Again")
    elif to_stack.is_empty() or from_stack.peek() < to_stack.peek():
      disk = from_stack.pop()
      to_stack.push(disk)
      num_user_moves += 1
      break
    else:
      print("\n\nInvalid Move. Try Again")

print(f"\n\nYou completed the game in {num_user_moves} moves, and the optimal number of moves is {num_optimal_moves}")
```

## Hash Maps
- Hash maps map keys to a related value(s) and are some of the most efficient data structures for retrieving stored data
- When you approach a problem that requires data retrieval, hash maps are often the best structure for the task
- Hash maps require a unique key to map to a single piece of data

### Hash Functions
- A hash funciton takes an input and returns an array index as the output.  In order to produce an index, the function must know the array length to always produce an index within the length
- The hash function takes the input, computes a value using a scoring metric (this is the hash), and returns the hash % array length
- Hash functions are also known as compression functions because they take a large range of inputs and return a defined subset of values (indices)

### Collisions
- A hash collision occurs when two different inputs hash to the same value which is very bad
- One strategy to resolve hash maps is called separate chaining.  When a value hashes to an index, add the data into a stored array at the hash index or a linked list
  - Saving keys: When using separate chaining it is typically a good idea to store the key that was used to produce the collision within the stored data to easily retrieve it later

### Hash map code example using open addressing
```
class HashMap:
  def __init__(self, array_size):
    self.array_size = array_size
    self.array = [None for item in range(array_size)]

  def hash(self, key, count_collisions=0):
    key_bytes = key.encode()
    hash_code = sum(key_bytes)
    return hash_code + count_collisions

  def compressor(self, hash_code):
    return hash_code % self.array_size

  def assign(self, key, value):
    array_index = self.compressor(self.hash(key))
    current_array_value = self.array[array_index]

    if current_array_value is None:
      self.array[array_index] = [key, value]
      return

    if current_array_value[0] == key:
      self.array[array_index] = [key, value]
      return

    # Collision!

    number_collisions = 1

    while(current_array_value[0] != key):
      new_hash_code = self.hash(key, number_collisions)
      new_array_index = self.compressor(new_hash_code)
      current_array_value = self.array[new_array_index]

      if current_array_value is None:
        self.array[new_array_index] = [key, value]
        return

      if current_array_value[0] == key:
        self.array[new_array_index] = [key, value]
        return

      number_collisions += 1

    return

  def retrieve(self, key):
    array_index = self.compressor(self.hash(key))
    possible_return_value = self.array[array_index]

    if possible_return_value is None:
      return None

    if possible_return_value[0] == key:
      return possible_return_value[1]

    retrieval_collisions = 1

    while (possible_return_value != key):
      new_hash_code = self.hash(key, retrieval_collisions)
      retrieving_array_index = self.compressor(new_hash_code)
      possible_return_value = self.array[retrieving_array_index]

      if possible_return_value is None:
        return None

      if possible_return_value[0] == key:
        return possible_return_value[1]

      retrieval_collisions += 1

    return
```

## Algorithms

### Recursion
- Recursion is the process of using a function to call itself.
- When using recursion you attempt to solve a problem by defining the problem in the terms of itself.
- Recursion is a broad and tricky concept to grasp but is incredibly useful and efficient.
- Recursion isn't as efficient as iteration due to overhead of the call stack
#### Pseudocode example
- Pseudocode example of recursion paired with it's iterative counterpart:
  ```
  // recursive
  function speller( string )
    if string is empty
      print "done"
    print first letter of string
    call speller with the given string minus the first letter

  // iterative
  function speller( string )
    for each letter in the string
      print the letter
    print "done"
  ```
- When using recursion you must remember the `Call Stack`.  When you are calling a recursive function, the inner most function (the last to be called) will be the first to resolve.
  - In the recursive pseudocode above if I were to swap the print and call lines you would end up with a completely different output.
    - Current output inputting "Nat":
      - N
      - a
      - t
      - done
    - Output with print and call lines flipped inputting "Nat":
      - done
      - t
      - a
      - N
  - This is due to the call stack.  In the current implementation we are printing and **THEN** calling the function again but in the swapped implementation we are calling **FIRST** and then printing meaning all subsequent calls will resolve before the prints.

#### The Base Case and Recursive Step
- The two fundamental aspects of recursion are the `Base Case` and the `Recursive Step`
- The `base case` is what determines if the function should continue calling itself or if it should finish execution and resolve the remaining function calls.
  - If you forget your base case or have an insufficient base case you will end up in the recursive equivalent of an infinite loop and the call stack will throw a stack overflow error
  - An example of a base case is if you were mimicing a for loop but with recursion.  If you wanted to do something 20 times, you will have the **INPUT** to the function act as your counting variable and it will not end until you have an input that reaches 20
- Think of a recursive step as an iteration of a for loop.  Each time the funciton is called it is a recursive step

### Algorithmic Complexity (Big-O)