```markdown
# The `Stack` Class: A Stack Implementation

This document describes the `Stack` class, which provides an implementation of the stack data structure. This implementation is versatile as it can be initialized using either our custom `Array_new` class or a `LinkedList` (assumed to be from a `linked_lists` module).

```python
from data_structures.linked_lists import LinkedList
from data_structures.array import Array_new
# Add features to handle linked lists

# Add features to handle linked lists

class Stack:
    def __init__(self, para):
      self.stack = para
      self.size = self.size_stack()

    def __str__(self):
      if type(self.stack) == Array_new:
        return f"{self.stack}"

    def push(self,newElement):
      """This insert an element at the top of the stack."""
      if type(self.stack) == Array_new:
        a = [newElement] + [s for s in self.stack]
        self.stack = Array_new(a)
        self.size += 1

      if type(self.stack) == LinkedList:
        self.stack.InsertAtBeg(newElement)
        self.size += 1


    def peek(self):
      """Return the top element of the stack without removing it."""
      if not self.isEmpty():
        if type(self.stack) == Array_new:
          return self.stack[0]
        elif type(self.stack) == LinkedList:
          return self.stack.access(0)
      else:
        raise IndexError("Empty stack")

    def pop_stack(self):
      """Remove and return the top element of the stack."""
      if type(self.stack) == Array_new:
        if not self.isEmpty():
          a = self.stack[0]
          self.stack = Array_new(self.stack[1:])
          self.size -= 1
          return a
        else:
          raise IndexError("pop from empty stack")

      if type(self.stack) == LinkedList:
        if not self.isEmpty():
          top_element = self.stack.access(0)
          self.stack.deleteItem(0)
          self.size -= 1
          return top_element
        else:
          raise IndexError("pop from empty stack")

    def top(self):
      """Alias for peek(). Return the top element of the stack without removing it."""
      return self.peek()

    def isEmpty(self):
      """Checks if the stack is empty."""
      return self.size_stack() == 0


    def size_stack(self):
      """Returns the current size of the stack."""
      if type(self.stack) == LinkedList:
        return self.stack.get_length()

      if type(self.stack) == Array_new:
        return len(self.stack)

    def display_stack(self):
      """Displays the elements of the stack."""
      print("Top -> ", end="")
      if type(self.stack) == LinkedList:
        self.stack.display()
      elif type(self.stack) == Array_new:
        for i in range(len(self.stack)):
          print(self.stack[i], end=" -> ")
        print("None")
```

## `__init__(self, para)`

- **Purpose:** This is the constructor for the `Stack` class. It initializes a new stack object based on the provided parameter.
- **Parameters:**
    - `para`: This parameter can be either an instance of the `Array_new` class or an instance of the `LinkedList` class. This allows the stack to be implemented using either of these underlying data structures.
- **Functionality:**
    - It sets the `self.stack` attribute to the provided `para`.
    - It initializes the `self.size` attribute by calling the `self.size_stack()` method to determine the initial size of the stack based on the underlying data structure.

## `__str__(self)`

- **Purpose:** This special method defines how the `Stack` object should be represented as a string.
- **Functionality:** Currently, it only provides a string representation if the underlying stack is an `Array_new` object, returning the string representation of that `Array_new` object.

## `push(self, newElement)`

- **Purpose:** Adds a `newElement` to the top of the stack.
- **Parameters:**
    - `newElement`: The element to be added to the stack.
- **Functionality:**
    - **If the stack is based on `Array_new`:** It creates a new `Array_new` with the `newElement` at the beginning, effectively pushing it onto the top. The `self.stack` is updated with this new array, and the `self.size` is incremented.
    - **If the stack is based on `LinkedList`:** It uses the `InsertAtBeg()` method of the `LinkedList` to add the `newElement` at the beginning (which represents the top of the stack), and the `self.size` is incremented.

## `peek(self)`

- **Purpose:** Returns the element at the top of the stack without removing it.
- **Functionality:**
    - It first checks if the stack is empty using `self.isEmpty()`. If it is, it raises an `IndexError`.
    - **If the stack is based on `Array_new`:** It returns the element at index `0`, which represents the top of the stack.
    - **If the stack is based on `LinkedList`:** It returns the element at the beginning (index `0`) using the `access()` method of the `LinkedList`.

## `pop_stack(self)`

- **Purpose:** Removes and returns the element at the top of the stack.
- **Functionality:**
    - It first checks if the stack is empty. If it is, it raises an `IndexError`.
    - **If the stack is based on `Array_new`:**
        - It retrieves the element at index `0` (the top).
        - It creates a new `Array_new` containing all elements from index `1` onwards, effectively removing the top element.
        - It updates `self.stack` with this new array and decrements `self.size`.
        - It returns the removed `top_element`.
    - **If the stack is based on `LinkedList`:**
        - It retrieves the element at index `0` (the top) using `access()`.
        - It uses the `deleteItem(0)` method of the `LinkedList` to remove the first element.
        - It decrements `self.size`.
        - It returns the removed `top_element`.

## `top(self)`

- **Purpose:** This method is an alias for `peek()`, providing an alternative name to retrieve the top element of the stack without removal.

## `isEmpty(self)`

- **Purpose:** Checks if the stack is currently empty.
- **Functionality:** It calls the `self.size_stack()` method and returns `True` if the size is 0, and `False` otherwise.

## `size_stack(self)`

- **Purpose:** Returns the current number of elements in the stack.
- **Functionality:**
    - **If the stack is based on `LinkedList`:** It returns the length of the linked list using the `get_length()` method.
    - **If the stack is based on `Array_new`:** It returns the number of elements in the array using the `len()` function.

## `display_stack(self)`

- **Purpose:** Displays the elements of the stack, indicating the top.
- **Functionality:**
    - It prints "Top -> " to indicate the top of the stack.
    - **If the stack is based on `LinkedList`:** It calls the `display()` method of the `LinkedList` to print its elements.
    - **If the stack is based on `Array_new`:** It iterates through the elements of the array and prints each element followed by " -> ", ending with "None" to signify the bottom of the stack.
```



## Example Usage of the `Stack` Class with `Array_new`

This section demonstrates how to create and manipulate a `Stack` object when it is initialized with an `Array_new` object.


```python
from data_structures.array import Array_new
from data_structures.stack import Stack 

# Create an Array_new object
para = Array_new([1, 2, 3, 4, 5])

# Create a Stack using the Array_new object
my_stack = Stack(para)

# Push elements onto the stack
my_stack.push(6)  # Push 6 at the beginning
my_stack.push(7)  # Push 7

# Display the stack
my_stack.display_stack()  # Output: Top -> 7 -> 6 -> 1 -> 2 -> 3 -> 4 -> 5 -> None

# Peek at the top element
top_element = my_stack.peek()
print(f"Top element: {top_element}")  # Output: Top element: 7

# Pop an element
popped_element = my_stack.pop_stack()
print(f"Popped element: {popped_element}")  # Output: Popped element: 7

# Display the stack again
my_stack.display_stack()  # Output: Top -> 6 -> 1 -> 2 -> 3 -> 4 -> 5 -> None
```

**Explanation of the Example:**

1.  **Creating an `Array_new` Object:**
    ```python
    para = Array_new([1, 2, 3, 4, 5])
    ```
    An instance of the `Array_new` class is created with initial elements `[1, 2, 3, 4, 5]`.

2.  **Creating a `Stack` Object:**
    ```python
    my_stack = Stack(para)
    ```
    A `Stack` object `my_stack` is created, initialized with the `para` (our `Array_new` object). This means the stack's underlying storage is an `Array_new`.

3.  **Pushing Elements:**
    ```python
    my_stack.push(6)  # Push 6 at the beginning
    my_stack.push(7)  # Push 7
    ```
    The `push()` method adds new elements to the top of the stack. Since the underlying structure is `Array_new`, the `push()` operation effectively inserts the new element at the beginning of the array. Therefore, `6` is added before `[1, 2, 3, 4, 5]`, resulting in `[6, 1, 2, 3, 4, 5]`, and then `7` is added before that, resulting in `[7, 6, 1, 2, 3, 4, 5]`.

4.  **Displaying the Stack:**
    ```python
    my_stack.display_stack()  # Output: Top -> 7 -> 6 -> 1 -> 2 -> 3 -> 4 -> 5 -> None
    ```
    The `display_stack()` method iterates through the `Array_new` and prints the elements, indicating the top of the stack (the first element).

5.  **Peeking at the Top Element:**
    ```python
    top_element = my_stack.peek()
    print(f"Top element: {top_element}")  # Output: Top element: 7
    ```
    The `peek()` method returns the element at the top of the stack (the first element in the `Array_new`) without removing it.

6.  **Popping an Element:**
    ```python
    popped_element = my_stack.pop_stack()
    print(f"Popped element: {popped_element}")  # Output: Popped element: 7
    ```
    The `pop_stack()` method removes and returns the element at the top of the stack (the first element in the `Array_new`).

7.  **Displaying the Stack Again:**
    ```python
    my_stack.display_stack()  # Output: Top -> 6 -> 1 -> 2 -> 3 -> 4 -> 5 -> None
    ```
    After the `pop()` operation, the top element (`7`) has been removed, and the stack now starts with `6`. The `display_stack()` method shows the updated stack.


## Example Usage of the `Stack` Class with `LinkedList`

This section demonstrates how to create and manipulate a `Stack` object when it is initialized with a `LinkedList` object. We assume that the `LinkedList` class (with `InsertAtEnd`, `InsertAtBeg`, `display`, `access`, and `deleteItem` methods) is available from the `data_structures.linked_lists` module.


```python
from data_structures.linked_lists import LinkedList
from data_structures.stack import Stack 

# Create a LinkedList object
my_linked_list = LinkedList(True)
my_linked_list.InsertAtEnd(1)
my_linked_list.InsertAtEnd(2)
my_linked_list.InsertAtEnd(3)


# Create a Stack using the LinkedList object
my_stack_ll = Stack(my_linked_list)

# Push elements onto the stack
my_stack_ll.push(4)  # Push 4 to the beginning (top of the stack)
my_stack_ll.push(5)  # Push 5 to the beginning (new top of the stack)


# Display the stack
my_stack_ll.display_stack()  # Output: Top -> 5<-->4<-->1<-->2<-->3<-->None

# Peek at the top element
top_element_ll = my_stack_ll.peek()
print(f"Top element: {top_element_ll}")  # Output: Top element: 5

# Pop an element from the stack
popped_element_ll = my_stack_ll.pop_stack()
print(f"Popped element: {popped_element_ll}")  # Output: Popped element: 5

# Display the stack again
my_stack_ll.display_stack()  # Output: Top -> 4<-->1<-->2<-->3<-->None
```

**Explanation of the Example:**

1.  **Creating a `LinkedList` Object:**
    ```python
    my_linked_list = LinkedList(True)
    my_linked_list.InsertAtEnd(1)
    my_linked_list.InsertAtEnd(2)
    my_linked_list.InsertAtEnd(3)
    ```
    An instance of the `LinkedList` class (assuming it supports doubly linked lists as indicated by `True`) is created, and elements `1`, `2`, and `3` are inserted at the end of the list. In a stack context using a linked list, the beginning of the list typically represents the top of the stack.

2.  **Creating a `Stack` Object with `LinkedList`:**
    ```python
    my_stack_ll = Stack(my_linked_list)
    ```
    A `Stack` object `my_stack_ll` is created, initialized with the `my_linked_list`. This means the stack's underlying storage is now a linked list.

3.  **Pushing Elements:**
    ```python
    my_stack_ll.push(4)  # Push 4 to the beginning
    my_stack_ll.push(5)  # Push 5 to the beginning
    ```
    The `push()` method, when the stack is based on a `LinkedList`, uses the `InsertAtBeg()` method of the linked list. This effectively adds the new element at the beginning of the list, making it the new top of the stack. So, `4` is added at the beginning, and then `5` is added at the very beginning.

4.  **Displaying the Stack:**
    ```python
    my_stack_ll.display_stack()  # Output: Top -> 5<-->4<-->1<-->2<-->3<-->None
    ```
    The `display_stack()` method, for a `LinkedList`-based stack, calls the `display()` method of the linked list. Assuming the `display()` method prints the list from head to tail, and the head represents the top of the stack, the output shows the elements in the order of the stack (top to bottom).

5.  **Peeking at the Top Element:**
    ```python
    top_element_ll = my_stack_ll.peek()
    print(f"Top element: {top_element_ll}")  # Output: Top element: 5
    ```
    The `peek()` method for a `LinkedList`-based stack uses `access(0)` to return the element at the beginning of the list (the top of the stack) without removing it.

6.  **Popping an Element:**
    ```python
    popped_element_ll = my_stack_ll.pop_stack()
    print(f"Popped element: {popped_element_ll}")  # Output: Popped element: 5
    ```
    The `pop_stack()` method for a `LinkedList`-based stack uses `deleteItem(0)` to remove the element at the beginning of the list (the top) and returns its value using `access(0)` before deletion.

7.  **Displaying the Stack Again:**
    ```python
    my_stack_ll.display_stack()  # Output: Top -> 4<-->1<-->2<-->3<-->None
    ```
    After the `pop()` operation, the top element (`5`) has been removed, and the new top of the stack is `4`. The `display_stack()` method shows the updated linked list representing the stack.
    ```