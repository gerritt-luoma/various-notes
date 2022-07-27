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
      - [Factorial using recursion](#factorial-using-recursion)
      - [Flattening lists with recursion](#flattening-lists-with-recursion)
      - [Fibonacci Sequence with Recursion](#fibonacci-sequence-with-recursion)
      - [Recursive vs Iterative Traversal](#recursive-vs-iterative-traversal)
    - [Algorithmic Complexity (Big-O)](#algorithmic-complexity-big-o)
      - [Big Theta ($\Theta$)](#big-theta-theta)
      - [Common runtimes](#common-runtimes)
      - [Big Omega ($\Omega$) and Big O (O)](#big-omega-omega-and-big-o-o)
      - [Adding runtimes](#adding-runtimes)
      - [Asymptotic Examples](#asymptotic-examples)
  - [Non Linear Data Structures](#non-linear-data-structures)
    - [Trees](#trees)
      - [Binary Search Trees](#binary-search-trees)
      - [Heaps](#heaps)
      - [Basic Info](#basic-info)
      - [Example of a Tree Node:](#example-of-a-tree-node)
    - [Binary Search Trees](#binary-search-trees-1)
      - [An example in code](#an-example-in-code)
    - [Heaps](#heaps-1)
      - [Min heap code example](#min-heap-code-example)
  - [Sorting Algorithms](#sorting-algorithms)
    - [Algorithmic Complexity of Covered Sorting Algs](#algorithmic-complexity-of-covered-sorting-algs)
    - [Bubblw Sort](#bubblw-sort)
    - [Merge Sort](#merge-sort)
    - [Quick Sort](#quick-sort)
    - [Radix Sort](#radix-sort)
  - [Graphs and Graph Traversal](#graphs-and-graph-traversal)
    - [Graph Basics](#graph-basics)
      - [Definitions](#definitions)
      - [Representing Graphs](#representing-graphs)
      - [Basic graph code example](#basic-graph-code-example)
    - [Graph Searches/Traversals](#graph-searchestraversals)
      - [Traversal Order](#traversal-order)
      - [Depth First Search (`DFS`) - $O(vertices + edges)$](#depth-first-search-dfs---overtices--edges)
      - [Breadth First Search (`BFS`) - $O(vertices + edges)$](#breadth-first-search-bfs---overtices--edges)
      - [Dijkstra's Algorithm - $O((V + E)logV)$](#dijkstras-algorithm---ov--elogv)
      - [A* Algorithm](#a-algorithm)
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

#### Factorial using recursion
```
def factorial(n):
  if n < 2:
    return 1
  return n * factorial(n - 1)
```

#### Flattening lists with recursion
```
def flatten(my_list):
  result = []
  for item in my_list:
    if isinstance(item, list):
      print("List found!")
      flat_list = flatten(item)
      result.extend(flat_list)
    else:
      result.append(item)
  return result
```

#### Fibonacci Sequence with Recursion
```
def fibonacci(n):
  if n == 1:
    return 1
  if n == 0:
    return 0
  return fibonacci(n-1) + fibonacci(n-2)
```

#### Recursive vs Iterative Traversal
- When searching through a linked list, the iterative approach to traversing through the LL is:
  ```
  def find_node_iteratively(self, value):
  current_node = self.head_node
 
  while current_node:
    if current_node.value == value:
      return current_node
    current_node = current_node.get_next_node()
 
  return None
  ```


### Algorithmic Complexity (Big-O)
- When looking at the speed and efficiency of a program or algorithm, we want to look at the number of instructions a computer needs to perform to complete the execution based on the size of the input
- We look at the size of the input as the value N.  If there is another input we'll consider it M and so on
- The types of asymptotic behaviors that we look at are the best, average, and worst cases for the program
  - The best case would be like a binary search finding the value on the first iteration
  - The average case is what would happen on the average of all runs of the algorithm
  - The worst case is like if a binary search doesn't find the value until the last iteration or never finds it at all
- We use asymptotic notation because not all computers operate at the same speed.  Your old mac from 1998 won't run at the same speed as a brand new $4000 gaming computer full of unnecessary RGB lights.  You use asymptotic notation to instead estimate the number of instructions needed to finish execution.

#### Big Theta ($\Theta$)
- `Big Theta` is the value used to denote the runtime of a program that only has one case of runtime
- An example of a program with one runtime is a for loop that prints out all the values of a list.  The runtime for this program will always be $\Theta(N)$
- Or a different example is taking an input and dividing it by 2 in a while loop until it equals 1.  This will always take $log{_2}{N}$ iterations but since we are working in asymptotic notiation we drop the constants and report it at $\Theta(log{N})$


#### Common runtimes
- $\Theta(1)$
  - This represents a **constant** runtime.  If your program/algorithm does the same thing regardless of input, it has a constant runtime
- $\Theta(log{N})$
  - This represents a **logorithmic** runtime.  This is the runtime of a lot of searching algorithms as they don't tend to check every value in the structure
- $\Theta(N)$
  - This represents a **linear** runtime.  This is typically the runtime if you iterate through an entire set of data
- $\Theta(N*log{N})$
  - This is a typical runtime of sorting algorithms
- $\Theta(N^2)$
  - This is **polynomial** runtime. This happens when you have nested for loops or iterate through a multi dimensional array
- $\Theta(2^N)$
  - This is an **exponential** runtime.  You will generally see this in recursive algorithms when calling the function multiple time in the same return statement
- $\Theta(N!)$
  - This is **factorial** runtime.  You see this when you generate all of the permutations of something

#### Big Omega ($\Omega$) and Big O (O)
- When a function/algorithm has multiple cases for the runtime we use `Big Omega` to designate the best case runtime
- For the worst case, we use `Big O`
- People typically only discuss the `Big O` runtime because you should always be planning for the **worst case** instead of the best or average case

#### Adding runtimes
- Sometimes a program has multiple things going on and you will need to add together the runtimes
- For example, if you iterate through a list and then use a while loop to divide a value until it equals 1, you are looking at 2 different runtimes in the same algorithm
  - In this case you have a runtime of $\Theta(N)$ for the for loop and $\Theta(log{N})$ for the while loop.
  - For the entire answer you can report $\Theta(N)$ + $\Theta(log{N})$ as the average runtime
  - When looking at the problem in `Big O` notation, you only report the slowest portion of the program which is $O(N)$


#### Asymptotic Examples
```
# log N
def count(N):
  count = 0
  while N > 1:
    N = N//2
    count += 1
  return count
```

```
# N
def find_max(linked_list):
  node = linked_list.get_head_node()
  max = node.get_value()
  while node:
    if max < node.get_value():
      max = node.get_value()
    node = node.get_next_node()
  return max
```

```
# N^2
def sort_linked_list(linked_list):
  new_linked_list = LinkedList()
  head = linked_list.get_head_node()
  while head:
    node = head
    max = node.get_value()
    while node:
      if max < node.get_value():
        max = node.get_value()
      node = node.get_next_node()
    new_linked_list.insert_beginning(max)
    linked_list.remove_node(max)
    head = linked_list.get_head_node()
  return new_linked_list
```

## Non Linear Data Structures

### Trees
- Tree data structures are used for storing data with a hierarchical structure
- They are built using nodes similar to that of a linked list but instead point to left and right nodes and their parent

#### Binary Search Trees
- Binary search trees are a tree that are ordered so that each element to the left of a value are less than the value and each element to the right has a greater value
- BSTs make searching for elements more efficient but they require some overhead work to keep them organized and balanced

#### Heaps
- Heaps are a different type of tree keep track of the min or maximum value in the tree.  These are referred to as max heaps and min heaps
- Heaps are actually a variation of a BST since they use the same ordering as BSTs
  
#### Basic Info
- Trees grow downwards from the root node 
- Each node in a tree points to nodes lower in the tree.  These are known as `children`
- Each node also points to the node higher up in the tree.  This is known as the `parent`
- When a node has no children it is known as a `leaf`
- If a node points to many children, it is known as a wide tree
- Deep trees are trees with many layers
- Whenever we traverse from a parent to a child we are going down another layer of the tree
- When counting down from the root to a leaf you are finding the `depth`
- When counting up from a leaf to the root you are finding the `height`


#### Example of a Tree Node:
```
class TreeNode:
  def __init__(self, value):
    self.value = value
    self.children = []

  def add_child(self, child_node):
    print(f"Adding {child_node.value}")
    self.children.append(child_node) 
    
  def remove_child(self, child_node):
    print(f"Removing {child_node.value} from {self.value}")
    self.children = [child for child in self.children if child is not child_node]

  # Traverse through all nodes and print value
  def traverse(self):
    nodes_to_visit = [self]
    while len(nodes_to_visit) > 0:
      current_node = nodes_to_visit.pop()
      print(current_node.value)
      nodes_to_visit += current_node.children
```

### Binary Search Trees
- BSTs are an efficient datastructure for fast storage and retrieval ($O(log{N})$)
- This tree structure is made up of one root node and each node points to at most 2 children
- These trees can either enforce that there can be no duplicate values or allow for them
- The left children of nodes are always LESS than the parent and right children of nodes are always GREATER than the parent

#### An example in code
```
class BinarySearchTree:
  def __init__(self, value, depth=1):
    self.value = value
    self.depth = depth
    self.left = None
    self.right = None

  def insert(self, value):
    if (value < self.value):
      if (self.left is None):
        self.left = BinarySearchTree(value, self.depth + 1)
        print(f'Tree node {value} added to the left of {self.value} at depth {self.depth + 1}')
      else:
        self.left.insert(value)
    else:
      if (self.right is None):
        self.right = BinarySearchTree(value, self.depth + 1)
        print(f'Tree node {value} added to the right of {self.value} at depth {self.depth + 1}')
      else:
        self.right.insert(value)
        
  def get_node_by_value(self, value):
    if (self.value == value):
      return self
    elif ((self.left is not None) and (value < self.value)):
      return self.left.get_node_by_value(value)
    elif ((self.right is not None) and (value >= self.value)):
      return self.right.get_node_by_value(value)
    else:
      return None
  
  def depth_first_traversal(self):
    if (self.left is not None):
      self.left.depth_first_traversal()
    print(f'Depth={self.depth}, Value={self.value}')
    if (self.right is not None):
      self.right.depth_first_traversal()
```

### Heaps
- Heaps are used to maintain a maximum or minimum value of a dataset
- When dealing with a min heap you need to focus on a few key parts:
  - They are similar to a BST
  - The value of a child node is always greater than or equal to the parent
  - The minimum value of the set is always the root
- Heaps are typically visualized as trees since it's easier to understand conceptually but when they are actually being implemented, we tend to use arrays/lists for performance
- When you fill the tree in from left to right you can find the index of list implementation by doing the following:
  - Left Child: $(index * 2) + 1$
  - Right Child: $(index * 2) + 2$
  - Parent: $(index - 1) // 2$
- When you are trying to add a value that will break the fundamental rules of the heap you must `heapify` it
- When you add the value to the bottom of the heap, proceed to swap it's spot with it's parent until the rules are no longer broken.  This is known as `heapifying up`
- When you remove the root node from the heap you must `heapify down` which is the process of finding the new minimum, setting it to the root, and maintaining order

#### Min heap code example
```
class MinHeap:
  def __init__(self):
    self.heap_list = [None]
    self.count = 0

  def parent_idx(self, idx):
    return idx // 2

  def left_child_idx(self, idx):
    return idx * 2

  def right_child_idx(self, idx):
    return idx * 2 + 1

  def child_present(self, idx):
    return self.left_child_idx(idx) <= self.count
  
  def retrieve_min(self):
    if self.count == 0:
      print("No items in heap")
      return None
    
    min = self.heap_list[1]
    self.heap_list[1] = self.heap_list[self.count]
    self.count -= 1
    self.heap_list.pop()
    self.heapify_down()
    return min

  def add(self, element):
    self.count += 1
    self.heap_list.append(element)
    self.heapify_up()


  def get_smaller_child_idx(self, idx):
    if self.right_child_idx(idx) > self.count:
      return self.left_child_idx(idx)
    else:
      left_child = self.heap_list[self.left_child_idx(idx)]
      right_child = self.heap_list[self.right_child_idx(idx)]
      if left_child < right_child:
        return self.left_child_idx(idx)
      else:
        return self.right_child_idx(idx)
    
  def heapify_up(self):
    idx = self.count
    swap_count = 0
    while self.parent_idx(idx) > 0:
      if self.heap_list[self.parent_idx(idx)] > self.heap_list[idx]:
        swap_count += 1
        tmp = self.heap_list[self.parent_idx(idx)]
        self.heap_list[self.parent_idx(idx)] = self.heap_list[idx]
        self.heap_list[idx] = tmp
      idx = self.parent_idx(idx)

    element_count = len(self.heap_list)
    if element_count > 10000:
      print("Heap of {0} elements restored with {1} swaps"
            .format(element_count, swap_count))
      print("")    
      
  def heapify_down(self):
    idx = 1
    # starts at 1 because we swapped first and last elements
    swap_count = 1
    while self.child_present(idx):
      smaller_child_idx = self.get_smaller_child_idx(idx)
      if self.heap_list[idx] > self.heap_list[smaller_child_idx]:
        swap_count += 1
        tmp = self.heap_list[smaller_child_idx]
        self.heap_list[smaller_child_idx] = self.heap_list[idx]
        self.heap_list[idx] = tmp
      idx = smaller_child_idx

    element_count = len(self.heap_list)
    if element_count >= 10000:
      print("Heap of {0} elements restored with {1} swaps"
            .format(element_count, swap_count))
      print("")  
```


## Sorting Algorithms

### Algorithmic Complexity of Covered Sorting Algs
|             | Best Case     | Worst Case    | Average Case  | Space Complexity |
| ----------- | ------------- | ------------- | ------------- | ---------------- |
| Bubble Sort | $O(N)$        | $O(N^2)$      | $O(N^2)$      | $O(1)            |
| Merge Sort  | $O(N*log{N})$ | $O(N*log{N})$ | $O(N*log{N})$ | $O(N)$           |
| Quick Sort  | $O(N*log{N})$ | $O(N^2)$      | $O(N*log{N})$ | $O(log{N})$      |
| Radix Sort  | $O(kN)$       | $O(kN)$       | $O(kN)$       | $O(N + k)        |
### Bubblw Sort
- Bubble sort is an introductory sorting algorithm to teach the basics of sorting algorithms
- This algorithm is implemented with 2 loops
  - An inner loop which is looping through the full structure comparing adjacent values and swapping them if they don't abide to the sorting criteria.  This loops `N-1` times
  - An outer loop that will loop `N` times because with every pass of the inner loop, we are guaranteed to have 1 more item placed in order
```
def bubble_sort(arr):
  iteration_count = 0
  n = len(arr)
  for i in range(n):
    # iterate through unplaced elements
    for idx in range(n - i - 1):
      if arr[idx] > arr[idx + 1]:
        arr[idx], arr[idx + 1] = arr[idx + 1], arr[idx]
```

### Merge Sort
- Merge sort is a divide and conquer algorithm that breaks the list into multiple sections, performs small swaps, and then merges them back together sorted
- Merge sort consists of 2 steps
  1.  Breaking the list into smaller sections known as `runs`.  This continues until we are left with `N` lists of length 1
  2.  Once we have broken all of our lists into length of 1, we begin to merge them back together in a sorted fashion
- Once we begin merging them back together, we will have a left list and a right list.  You iterate through each list comparing the elements and inserting them in a sorted manner
- You only merge together presorted lists.  This is why we break the list down to many lists of length one
- Merge sort is actually comprised of two functions!
```
def merge_sort(items):
  if len(items) <= 1:
    return items

  middle_index = len(items) // 2
  left_split = items[:middle_index]
  right_split = items[middle_index:]

  left_sorted = merge_sort(left_split)
  right_sorted = merge_sort(right_split)

  return merge(left_sorted, right_sorted)

def merge(left, right):
  result = []

  while (left and right):
    if left[0] < right[0]:
      result.append(left[0])
      left.pop(0)
    else:
      result.append(right[0])
      right.pop(0)

  if left:
    result += left
  if right:
    result += right

  return result
```


### Quick Sort
- Quick sort is a recursive comparison sorting algorithm
- It also uses the divide and conquer strategy similar to merge sort
- The array is once again divided until it is a set of N arrays of length 1
- How it works:
  1.  Choose a pivot element.  Every other element will be compared to this one
  2.  Separate the list into 3 sub lists:
      1.  A list of elements **smaller than** the pivot
      2.  A list containing the pivot itself
      3.  A list containing elements **larger than** the pivot
  3.  Repeate step 2 until the sub arrays contain 0 or 1 elements
  4.  You then merge the sub lists back into the original list
- This algorithm produces a sorted mutation of the original list

```
from random import randrange, shuffle

def quicksort(list, start, end):
  if start >= end:
    return
  print("Running quicksort on {0}".format(list[start: end + 1]))
  
  # select random element to be pivot
  pivot_idx = randrange(start, end + 1)
  pivot_element = list[pivot_idx]

  # swap random element with last element in sub-lists
  list[end], list[pivot_idx] = list[pivot_idx], list[end]

  # tracks all elements which should be lesser than the pivot
  less_than_pointer = start
  
  for i in range(start, end):
    if list[i] < pivot_element:
      # swap element to the right-most portion of lesser elements
      list[i], list[less_than_pointer] = list[less_than_pointer], list[i]
      less_than_pointer += 1
  # move pivot element to the right-most portion of lesser elements
  list[end], list[less_than_pointer] = list[less_than_pointer], list[end]
  # recursively sort left and right sub-lists
  quicksort(list, start, less_than_pointer - 1)
  quicksort(list, less_than_pointer + 1, end)
```

### Radix Sort
- Radix sort is a non comparison sort managing to sort lists of integers without performing any comparisons
- Radix sort uses the base number of the desired numbering system to perform comparisons
- Radix sort has 2 variants.  Most significant digit (`MSD`) and Least significant digit (`LSD`)
- Numbers are bucketed based on the value of digits.  The comparisons are made from left to right with `MSD` and right to left with `LSD`
- This is only used on numbers

```
def radix_sort(to_be_sorted):
  maximum_value = max(to_be_sorted)
  max_exponent = len(str(maximum_value))
  being_sorted = to_be_sorted[:]

  for exponent in range(max_exponent):
    position = exponent + 1
    index = -position

    digits = [[] for i in range(10)]

    for number in being_sorted:
      number_as_a_string = str(number)
      try:
        digit = number_as_a_string[index]
        digit = int(digit)

      except IndexError:
        digit = 0
      
      digits[digit].append(number)
    
    being_sorted = []
    for numeral in digits:
      being_sorted.extend(numeral)

  return being_sorted
```

## Graphs and Graph Traversal

### Graph Basics
- Graphs are a data structure used to model networks
- Graphs are composed of vertices (Nodes) and edges which are the connections between to vertices
- A basic image of a graph:

![Graph image pulled from web.cecs.pdx.edu](http://web.cecs.pdx.edu/~sheard/course/Cs163/Graphics/graph1.png)
- You can use graphs to model streets to destinations, subway stations, plane flights, etc
- Graphs have varying levels of connections.  The larger the ratio between edges and connections is, the more connected the graph is
- If the graph represents a social network, the people are the vertices while the edges are friendships

#### Definitions
- When the edge goes both directions it is considered a `bi directional` edge
- When the edges only goes one direction, it is considered a `directed` graph
- When you can connect between 2 vertices over any number of edges this is known as a `path`
- When no path exists between 2 vertices, the graph is considered `disconnected`
  - In the image above the graph would be disconnected if we removed the edges between 4-5 and 3-2
- When driving from point A to point B you travel a specific distance.  In the terms of graphs, this distance is the `weight` of the edge
  - When travelling from point A to point B on a graph, you will want to tally the total weight to find to overall cost of the path

#### Representing Graphs
- The vertex-edge relationship of a graph is typically represented in two ways: an adjacency list or an adjacency matrix
- An adjacency matrix is a table where the it is an $NxN$ size
- Each node is represented on both the x and y axes.  Each node is represented twice because the edges can go both ways


#### Basic graph code example
```
class Vertex:
  def __init__(self, value):
    self.value = value
    self.edges = {}

  def add_edge(self, vertex, weight = 0):
    self.edges[vertex] = weight

  def get_edges(self):
    return list(self.edges.keys())
```

```
class Graph:
  def __init__(self, directed = False):
    self.graph_dict = {}
    self.directed = directed

  def add_vertex(self, vertex):
    self.graph_dict[vertex.value] = vertex

  def add_edge(self, from_vertex, to_vertex, weight = 0):
    self.graph_dict[from_vertex.value].add_edge(to_vertex.value, weight)
    if not self.directed:
      self.graph_dict[to_vertex.value].add_edge(from_vertex.value, weight)

  def find_path(self, start_vertex, end_vertex):
    start = [start_vertex]
    seen = {}
    while len(start) > 0:
      current_vertex = start.pop(0)
      seen[current_vertex] = True
      print("Visiting " + current_vertex)
      if current_vertex == end_vertex:
        return True
      else:
        vertices_to_visit = set(self.graph_dict[current_vertex].edges.keys())
        start += [vertex for vertex in vertices_to_visit if vertex not in seen]
    return False
```

### Graph Searches/Traversals

#### Traversal Order
- There are 3 main traversal order that are used when traversing through graphs
  1.  `Preorder`: Preorder is when each vertex is added to the `visited list` and added to the `output list` **BEFORE** getting *added* to the stack
  2.  `Postorder`: Postorder is when each vertex is added to the `visited list` and added to the `output list` **AFTER** it is *popped* off the stack
  3.  `Reverse postorder`: Also known as `Topological Sort`, which returns an output list which is the exact reverse of the post order output list


#### Depth First Search (`DFS`) - $O(vertices + edges)$
- A depth first graph search follows a path all the way to the end the graph before trying a new path
- Common uses:
  - Finding a path between 2 vertices
  - Detecting cycles
  - Topological sorting
  - Solving problems with a single correct answer (like sudoku)
- Typically uses recursion or a stack
```
def dfs(graph, current_vertex, target_value, visited=None):
  if visited is None:
    visited = []
	
  visited.append(current_vertex)
  
  if current_vertex == target_value:
    return visited
	
  # Add your recursive case here:
  for neighbor in graph[current_vertex]:
    if neighbor not in visited:
      path = dfs(graph, neighbor, target_value, visited)
      if path:
        return path
```

#### Breadth First Search (`BFS`) - $O(vertices + edges)$
- A breadth first search on a graph checks all of the neighboring vertices before moving another level down
- This is very inefficient when trying to find a path between 2 points but is a good way of trying to find the **SHORTEST** path between them
- Helpful for finding directions between two vertices
- Typically uses a queue
```
def bfs(graph, start_vertex, target_value):
  path = [start_vertex]
  vertex_and_path = [start_vertex, path]
  bfs_queue = [vertex_and_path]
  visited = set()
  
  while bfs_queue:
    current_vertex, path = bfs_queue.pop(0)
    visited.add(current_vertex)
    
    for neighbor in graph[current_vertex]:
      # Finish the function here:
      if neighbor not in visited:
        if neighbor is target_value:
          return path + [neighbor]
        else:
          bfs_queue.append([neighbor, path + [neighbor]])
```

#### Dijkstra's Algorithm - $O((V + E)logV)$
- Dijkstra's algorithm is used to find the **SHORTEST** distance from one given path to every other point in a weighted graph
- The algorithm keeps track of all distances and updates these distances during a `BFS`
- Very common algoritm for finding the quickest path from one point to another
- Overview of how Dijkstra's works:
  1. Instantiate a dict which will map vertices to their disctance from the start vertex
  2. Assign the start vertex with a distance of 0 on a min heap
  3. Assign every other vertex a distance of infinity in the min heap
  4. Remove the vertex with the smallest distance from min heap and set to current vertex
  5. With the current vertex look at adjacent vertexes and calculate distance from start (total distance + edge weight)
  6. If this is less than the current distance, replace the current distance
  7. Once the heap is empty return the distances

```
from heapq import heappop, heappush
from math import inf

def dijkstras(graph, start):
  distances = {}
  
  for vertex in graph:
    distances[vertex] = inf
    
  distances[start] = 0
  vertices_to_explore = [(0, start)]
  
  while vertices_to_explore:
    current_distance, current_vertex = heappop(vertices_to_explore)
    
    for neighbor, edge_weight in graph[current_vertex]:
      new_distance = current_distance + edge_weight
      
      if new_distance < distances[neighbor]:
        distances[neighbor] = new_distance
        heappush(vertices_to_explore, (new_distance, neighbor))
        
  return distances
```


#### A* Algorithm
- A* is used to not find the shortest path to all points from point, but is instead used to find the shortest path from one point to another point
- This avoids searching for other connecting path which saves a lot of time
- Instead of checking the distance up to the current vertex like in Dijkstra's, it checks the distance to the current vertex + the estimated distance to the target
- This estimated distance is called the `heuristic` and is calculated with pythagorean theorem
  - $d = \sqrt{(x_1-x_2)^2+(y_1+y_2)^2}$
- Changes from Dijkstra's:
  1. Add a *target* to the search along side the *start*
  2. Gather possible optimal paths and identify a **single** shortest path
  3. Implement a `heuristic` that estimates the likely distance remaining

```
from math import inf, sqrt
from heapq import heappop, heappush

def heuristic(start, target):
  x_distance = abs(start.position[0] - target.position[0])**2
  y_distance = abs(start.position[1] - target.position[1])**2
  return sqrt(x_distance + y_distance)

def a_star(graph, start, target):
  count = 0
  paths_and_distances = {}

  for vertex in graph:
    paths_and_distances[vertex] = [inf, [start.name]]
  
  paths_and_distances[start][0] = 0
  vertices_to_explore = [(0, start)]
  while vertices_to_explore and paths_and_distances[target][0] == inf:
    current_distance, current_vertex = heappop(vertices_to_explore)
    for neighbor, edge_weight in graph[current_vertex]:
      new_distance = current_distance + edge_weight + heuristic(neighbor, target)
      new_path = paths_and_distances[current_vertex][1] + [neighbor.name]
      
      if new_distance < paths_and_distances[neighbor][0]:
        paths_and_distances[neighbor][0] = new_distance
        paths_and_distances[neighbor][1] = new_path
        heappush(vertices_to_explore, (new_distance, neighbor))
        count += 1
  return paths_and_distances[target][1]
```