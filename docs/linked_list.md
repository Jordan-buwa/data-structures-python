```markdown
# The `Node` and `LinkedList` Classes for Linked List Implementation

This document explains the `Node` and `LinkedList` classes, which provide a comprehensive implementation of linked list data structures, supporting both singly and doubly linked lists.

## `Node` Class

The `Node` class represents a single node in the linked list. Each node contains a `value` and references to the `next` node (for singly linked lists) and optionally to the `prev` node (for doubly linked lists).

```python
class Node:
  def __init__(self, value, next = None, prev = None):
    self.value = value
    self.next = next
    self.prev = prev
```

### `__init__(self, value, next=None, prev=None)`

- **Purpose:** This is the constructor for the `Node` class. It initializes a new node.
- **Parameters:**
    - `value`: The data to be stored in this node.
    - `next`: An optional reference to the next node in the list. Defaults to `None`.
    - `prev`: An optional reference to the previous node in the list (used for doubly linked lists). Defaults to `None`.
- **Functionality:** When a `Node` object is created, this method sets the `value`, `next`, and `prev` attributes to the provided values.

## `LinkedList` Class

The `LinkedList` class implements the linked list data structure, providing methods for insertion, deletion, traversal, searching, and other common linked list operations. It supports both singly and doubly linked lists through the `double` flag in the constructor.

```python
class LinkedList:
  def __init__(self,double = False):
    self.head = None
    self.double = double

  # Inserting a node at the beginning of the list
  def InsertAtBeg(self, item):
    if self.head:
      new = Node(item)
      new.next = self.head
      if self.double:
        self.head.prev = new
      self.head = new
    else:
      self.head = Node(item)

  # Inserting a node at a particular position of the list
  def InsertAtPos(self, item, index):
    node = Node(item)
    if ((not self.head) and (index == 0)) or (index == 0):
      self.InsertAtBeg(item)
    else:
      i = 0
      temp = self.head

      while i < index and temp.next != None:
        i += 1
        prev = temp
        temp = temp.next

      if i == index:
        node.next = temp
        prev.next = node
        if self.double:
          temp.prev = node
          node.prev = prev

      elif index == i+1:
        self.InsertAtEnd(item)
      else:
        raise IndexError("This index is out of bounds")


  # Inserting a node at the end of the list
  def InsertAtEnd(self, item):
    last = Node(item)
    if self.head:
      temp = self.head
      while temp.next:
        prev = temp
        temp = temp.next
      temp.next = last
      if self.double:
        last.prev = temp
    else:
      self.head = last

  # Deleting a node with its index
  def deleteItem(self, index):
    i = 0
    tem = self.head
    if not self.head:
      raise IndexError("The list is empty")
      pass
    else:
      if index == 0:
        self.head = self.head.next
      while tem.next and i < index:
        prev = tem
        tem = tem.next
        i += 1
      if i == index and index != 0:
        if self.double:
          tem.next.prev = prev
        prev.next = tem.next
      elif not tem.next:
        raise IndexError(f'There is less than {index} elements in the linked list')

  # Get_length: count the number of nodes in the list

  def get_length(self):
    if not self.head:
      return 0
    else:
      i = 1
      temp = self.head
      while temp.next:
        i += 1
        temp = temp.next
      return i

  # Access: return the value of the node at the given position
  def access(self, index):
    if self.get_length() == 0 :
      print(f"The list is empty")
    elif self.get_length() <= index:
     raise IndexError("Index out of bound")
    else:
      temp = self.head
      for k in range(index):
        temp = temp.next
      return temp.value


  # Allow subscription

  def __getitem__(self, index):
      if isinstance(index, int):
      # Handle single index subscription
        if index >= 0:
          return self.access(index)
        else:
          if abs(index) <= self.get_length():
            return self.access(self.get_length() + index)
          else:
            raise IndexError("Index out of bound")
      else:
        raise TypeError("Invalid index type")

  # Search: look for a node with a specific value or property

  def search(self, key):
    '''Returns a list of indices of the nodes with value = key
    The list is empty if there is no node with value = key'''

    if self.get_length() == 0:
      raise IndexError(f"The list is empty")
    else:
      indices = []
      i = 0
      temp = self.head
      while temp is not None:
        if temp.value == key:
          indices.append(i)
        temp = temp.next
        i += 1
      return indices

  # Reverse the linked list

  def reverse_list(self):
    if self.IsEmpty():
      raise IndexError("The list is empty")
    else:
      new_list = LinkedList(self.double)
      temp = self.head

      while temp.next:
        new_list.InsertAtBeg(temp.value)
        temp = temp.next
      new_list.InsertAtBeg(temp.value)
      return new_list

  # Update a value at a particular position
  def update(self, new_val, pos):
    n = self.get_length()
    if n != 0:
      tem = self.head
      if pos <= n and pos >= 0 or (pos < 0 and pos >= -n):
        if pos < 0 :
          for i in range(n + pos):
            tem = tem.next
          tem.value = new_val
        else:
          for i in range(pos):
            tem = tem.next
          tem.value = new_val
      else:
        raise IndexError(f"Index {pos} out of range")
    else:
      raise IndexError(f"Cannot update element in an empty list")
  def IsEmpty(self):
    return  self.get_length() == 0

  def last_node(self):
    if self.head is None:
      raise IndexError("The linked list is empty")
    else:
      tem = self.head
      while(tem.next):
        tem = tem.next
      return tem

  def concatenate(self, L1, L2):
    pass

  def display(self):
      node = self.head

      a = "<-->" if self.double else "->"
      while node:
          print(node.value, end = a)
          node = node.next
      print('')
```

### `__init__(self, double=False)`

- **Purpose:** This is the constructor for the `LinkedList` class. It initializes an empty linked list.
- **Parameters:**
    - `double`: A boolean flag indicating whether the linked list should be doubly linked (`True`) or singly linked (`False`). Defaults to `False` (singly linked).
- **Functionality:** It sets the `head` attribute to `None` (indicating an empty list) and stores the `double` flag.

### `InsertAtBeg(self, item)`

- **Purpose:** Inserts a new node with the given `item` at the beginning of the list.
- **Parameters:**
    - `item`: The value to be inserted into the new node.
- **Functionality:**
    - If the list is not empty, it creates a new `Node`, sets its `next` pointer to the current `head`, and updates the `prev` pointer of the old `head` if it's a doubly linked list. Finally, it sets the `head` to the new node.
    - If the list is empty, it creates a new `Node` and sets it as the `head`.

### `InsertAtPos(self, item, index)`

- **Purpose:** Inserts a new node with the given `item` at a specific `index` in the list.
- **Parameters:**
    - `item`: The value to be inserted.
    - `index`: The position at which to insert the new node (0-based).
- **Functionality:**
    - If the list is empty and the index is 0, or if the index is 0, it calls `InsertAtBeg`.
    - Otherwise, it iterates through the list until it reaches the specified `index` or the end of the list.
    - If the `index` is reached, it inserts the new node at that position, updating the `next` and `prev` pointers of the surrounding nodes if it's a doubly linked list.
    - If the `index` is one position beyond the current end, it calls `InsertAtEnd`.
    - If the `index` is out of bounds, it raises an `IndexError`.

### `InsertAtEnd(self, item)`

- **Purpose:** Inserts a new node with the given `item` at the end of the list.
- **Parameters:**
    - `item`: The value to be inserted.
- **Functionality:**
    - If the list is not empty, it traverses to the last node and appends the new node, updating the `prev` pointer of the new node if it's a doubly linked list.
    - If the list is empty, it creates a new `Node` and sets it as the `head`.

### `deleteItem(self, index)`

- **Purpose:** Deletes the node at the specified `index` from the list.
- **Parameters:**
    - `index`: The position of the node to delete (0-based).
- **Functionality:**
    - If the list is empty, it raises an `IndexError`.
    - If the `index` is 0, it updates the `head` to the next node.
    - Otherwise, it iterates to the node at the given `index`. Once found, it updates the `next` pointer of the previous node to skip the current node. If it's a doubly linked list, it also updates the `prev` pointer of the next node.
    - If the `index` is out of bounds, it raises an `IndexError`.

### `get_length(self)`

- **Purpose:** Returns the number of nodes in the linked list.
- **Functionality:** It traverses the list and counts the number of nodes.

### `access(self, index)`

- **Purpose:** Returns the value of the node at the specified `index`.
- **Parameters:**
    - `index`: The position of the node to access (0-based).
- **Functionality:**
    - If the list is empty or the `index` is out of bounds, it raises an `IndexError`.
    - Otherwise, it traverses to the node at the given `index` and returns its `value`.

### `__getitem__(self, index)`

- **Purpose:** Enables accessing elements of the linked list using index-based subscription (e.g., `list[0]`).
- **Parameters:**
    - `index`: The index of the element to access. Supports both positive and negative indexing.
- **Functionality:**
    - If the `index` is a non-negative integer, it calls the `access()` method.
    - If the `index` is a negative integer, it calculates the corresponding positive index from the end of the list and calls `access()`.
    - If the `index` is out of bounds, it raises an `IndexError`.
    - If the `index` is not an integer, it raises a `TypeError`.

### `search(self, key)`

- **Purpose:** Searches for nodes with a specific `key` (value) and returns a list of their indices.
- **Parameters:**
    - `key`: The value to search for.
- **Functionality:**
    - If the list is empty, it raises an `IndexError`.
    - Otherwise, it traverses the list and appends the index of each node whose `value` matches the `key` to a list.
    - It returns the list of indices.

### `reverse_list(self)`

- **Purpose:** Creates and returns a new linked list that is the reverse of the original list.
- **Functionality:** It iterates through the original list and inserts each node's value at the beginning of the new list, effectively reversing the order. The `double` property of the new list is the same as the original.

### `update(self, new_val, pos)`

- **Purpose:** Updates the value of the node at a particular `pos` (index) with `new_val`.
- **Parameters:**
    - `new_val`: The new value to set.
    - `pos`: The index of the node to update (supports positive and negative indexing).
- **Functionality:**
    - If the list is not empty and the `pos` is within the valid range, it traverses to the node at the given `pos` and updates its `value`.
    - If the list is empty or the `pos` is out of bounds, it raises an `IndexError`.

### `IsEmpty(self)`

- **Purpose:** Returns `True` if the linked list is empty (head is `None`), and `False` otherwise.

### `last_node(self)`

- **Purpose:** Returns the last node in the linked list.
- **Functionality:** It traverses the list until it reaches the last node (the node whose `next` pointer is `None`). If the list is empty, it raises an `IndexError`.

### `display(self)`

- **Purpose:** Prints the elements of the linked list.
- **Functionality:** It traverses the list and prints the `value` of each node. For doubly linked lists, it indicates the bidirectional connections (`<-->`), and for singly linked lists, it indicates unidirectional connections (`->`). It ends with a newline character.





## Example Usage of the `LinkedList` Class

This section provides practical examples of how to create and interact with `LinkedList` objects, demonstrating the usage of various methods defined in the class.


```python
# Create a new LinkedList
my_list = LinkedList()

# Insert elements at the beginning
my_list.InsertAtBeg(3)
my_list.InsertAtBeg(2)
my_list.InsertAtBeg(1)

# Insert an element at a specific position
my_list.InsertAtPos(4, 2)  # Insert 4 at index 2

# Insert an element at the end
my_list.InsertAtEnd(5)

# Display the list
my_list.display()  # Output: 1->2->4->3->5->

# Access an element by index
element = my_list[2]  # Access element at index 2
print(f"Element at index 2: {element}")  # Output: Element at index 2: 4

# Get the length of the list
length = my_list.get_length()
print(f"Length of the list: {length}")  # Output: Length of the list: 5

# Search for an element
indices = my_list.search(3)  # Search for the element 3
print(f"Indices of element 3: {indices}")  # Output: Indices of element 3: [3]

# Delete an element by index
my_list.deleteItem(2)  # Delete element at index 2

# Display the list after deletion
my_list.display()  # Output: 1->2->3->5->

# Reverse the list
reversed_list = my_list.reverse_list()
reversed_list.display()  # Output: 5->3->2->1->


# Update the value at a particular position
my_list.update(10, 1)
my_list.display() # Output: 1->10->3->5->
```

**Explanation of the Example:**

1.  **Creating a `LinkedList` Object:**
    ```python
    my_list = LinkedList()
    ```
    An instance of the `LinkedList` class is created. By default, it's initialized as a singly linked list (`double=False`).

2.  **Inserting at the Beginning:**
    ```python
    my_list.InsertAtBeg(3)
    my_list.InsertAtBeg(2)
    my_list.InsertAtBeg(1)
    ```
    The `InsertAtBeg()` method adds new nodes at the beginning of the list. So, the list becomes `1 -> 2 -> 3`.

3.  **Inserting at a Specific Position:**
    ```python
    my_list.InsertAtPos(4, 2)  # Insert 4 at index 2
    ```
    The `InsertAtPos()` method inserts a new node with the value `4` at index `2` (0-based). The list becomes `1 -> 2 -> 4 -> 3`.

4.  **Inserting at the End:**
    ```python
    my_list.InsertAtEnd(5)
    ```
    The `InsertAtEnd()` method adds a new node with the value `5` at the end of the list. The list becomes `1 -> 2 -> 4 -> 3 -> 5`.

5.  **Displaying the List:**
    ```python
    my_list.display()  # Output: 1->2->4->3->5->
    ```
    The `display()` method prints the values of the nodes in the list, separated by `->` for a singly linked list.

6.  **Accessing an Element by Index:**
    ```python
    element = my_list[2]  # Access element at index 2
    print(f"Element at index 2: {element}")  # Output: Element at index 2: 4
    ```
    The `__getitem__()` method allows accessing elements using index-based subscription. Here, it retrieves the element at index `2`, which is `4`.

7.  **Getting the Length:**
    ```python
    length = my_list.get_length()
    print(f"Length of the list: {length}")  # Output: Length of the list: 5
    ```
    The `get_length()` method returns the number of nodes in the list.

8.  **Searching for an Element:**
    ```python
    indices = my_list.search(3)  # Search for the element 3
    print(f"Indices of element 3: {indices}")  # Output: Indices of element 3: [3]
    ```
    The `search()` method finds all occurrences of a given value and returns a list of their indices. Here, the value `3` is found at index `3`.

9.  **Deleting an Element by Index:**
    ```python
    my_list.deleteItem(2)  # Delete element at index 2
    ```
    The `deleteItem()` method removes the node at the specified index. Here, the node at index `2` (which was `4`) is removed, and the list becomes `1 -> 2 -> 3 -> 5`.

10. **Displaying After Deletion:**
    ```python
    my_list.display()  # Output: 1->2->3->5->
    ```
    The `display()` method shows the list after the deletion.

11. **Reversing the List:**
    ```python
    reversed_list = my_list.reverse_list()
    reversed_list.display()  # Output: 5->3->2->1->
    ```
    The `reverse_list()` method creates a new linked list with the nodes in reverse order.

12. **Updating a Value:**
    ```python
    my_list.update(10, 1)
    my_list.display() # Output: 1->10->3->5->
    ```
    The `update()` method changes the value of the node at the specified index. Here, the value at index `1` (which was `2`) is updated to `10`.
```