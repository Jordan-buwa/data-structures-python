```markdown
# The `Queue` Class: A Queue Implementation using `LinkedList`

This page describes the `Queue` class, which implements a queue data structure using our custom `LinkedList` class as its underlying storage.

```python
from .linked_lists import LinkedList

class Queue:
    """N is the max size of our queue"""
    N = 20


    def __init__(self, para=None):  # Initialize with an optional LinkedList
        if para is None:
            self.queue = LinkedList()  # Create an empty LinkedList if not provided
        else:
            self.queue = para  # Use the provided LinkedList
        self.size = self.queue.get_length()  # Initialize size

    def enqueue(self, new):
        if not self.isFull():
            self.queue.InsertAtEnd(new)  # Use InsertAtEnd for LinkedList
            self.size += 1  # Update size
        else:
            raise IndexError("The queue is full")

    def isNull(self):
        return self.size == 0  # Use size attribute

    def dequeue(self):
        if not self.isNull():
            removed_item = self.queue[0]  # Access the front
            self.queue.deleteItem(0)  # Remove from the front using deleteItem
            self.size -= 1  # Update size
            return removed_item
        else:
            raise IndexError("The queue is empty")

    def rear(self):
        if not self.isNull():
            return self.queue.last_node().value  # Access the last node's value
        else:
            return None

    def peek(self):
        if not self.isNull():
            return self.queue[0]  # Access the front
        else:
            return None

    def isFull(self):
        return self.size == self.__class__.N

    def display_queue(self):
        self.queue.display()  # LinkedList's display method
```

## Class Definition

The `Queue` class implements a First-In, First-Out (FIFO) data structure, where elements are added to the rear and removed from the front. It utilizes a `LinkedList` to store the queue elements.

## Class Attributes

- `N = 20`: A class-level constant defining the maximum size of the queue.

## `__init__(self, para=None)`

- **Purpose:** This is the constructor for the `Queue` class. It initializes a new queue object.
- **Parameters:**
    - `para`: An optional `LinkedList` object. If provided, this linked list will be used as the underlying storage for the queue. If not provided, a new empty `LinkedList` is created.
- **Functionality:**
    - It initializes the `self.queue` attribute with either the provided `LinkedList` or a new empty one.
    - It initializes the `self.size` attribute to the current length of the `self.queue` using the `get_length()` method of the `LinkedList`.

## `enqueue(self, new)`

- **Purpose:** Adds a new element to the rear (end) of the queue.
- **Parameters:**
    - `new`: The element to be added to the queue.
- **Functionality:**
    - It first checks if the queue is full using the `self.isFull()` method.
    - If the queue is not full, it uses the `InsertAtEnd()` method of the underlying `LinkedList` to add the `new` element at the end of the list (which represents the rear of the queue).
    - It then increments the `self.size` of the queue.
    - If the queue is full, it raises an `IndexError` indicating that the queue is full.

## `isNull(self)`

- **Purpose:** Checks if the queue is empty.
- **Functionality:** It returns `True` if the `self.size` of the queue is 0, and `False` otherwise.

## `dequeue(self)`

- **Purpose:** Removes and returns the element from the front of the queue (the element that was added earliest).
- **Functionality:**
    - It first checks if the queue is empty using `self.isNull()`.
    - If the queue is not empty, it retrieves the element at the front of the `LinkedList` using index `0` (`self.queue[0]`).
    - It then removes this element from the front of the `LinkedList` using the `deleteItem(0)` method.
    - It decrements the `self.size` of the queue.
    - It returns the `removed_item`.
    - If the queue is empty, it raises an `IndexError` indicating that the queue is empty.

## `rear(self)`

- **Purpose:** Returns the element at the rear (end) of the queue without removing it.
- **Functionality:**
    - It first checks if the queue is empty using `self.isNull()`.
    - If the queue is not empty, it accesses the last node of the `LinkedList` using `self.queue.last_node()` and returns its `value`.
    - If the queue is empty, it returns `None`.

## `peek(self)`

- **Purpose:** Returns the element at the front of the queue without removing it.
- **Functionality:**
    - It first checks if the queue is empty using `self.isNull()`.
    - If the queue is not empty, it accesses the element at the front of the `LinkedList` using index `0` (`self.queue[0]`) and returns it.
    - If the queue is empty, it returns `None`.

## `isFull(self)`

- **Purpose:** Checks if the queue is full (reached its maximum capacity).
- **Functionality:** It compares the current `self.size` of the queue with the maximum size `self.__class__.N` (which is 20). It returns `True` if the queue is full and `False` otherwise.

## `display_queue(self)`

- **Purpose:** Displays the elements currently in the queue.
- **Functionality:** It calls the `display()` method of the underlying `LinkedList` to print the elements of the queue. The order of elements in the linked list represents the order in the queue (front to rear).


```markdown
## Example Usage of the `Queue` Class

This section demonstrates how to create and interact with `Queue` objects, showcasing the enqueue, dequeue, peek, and isEmpty operations.

```python
from data_structures.queue import Queue # Assuming your Queue class is in 'queue.py'
from data_structures.linked_lists import LinkedList

# Initialize a queue using a LinkedList (implicitly, as no LinkedList is passed)
my_queue = Queue()

# Enqueue elements
my_queue.enqueue(10)
my_queue.enqueue(20)
my_queue.enqueue(30)

# Display the queue
my_queue.display_queue()  # Output: 10->20->30->

# Dequeue an element
removed_element = my_queue.dequeue()
print(f"Removed element: {removed_element}")  # Output: Removed element: 10

# Display the queue after dequeue
my_queue.display_queue()  # Output: 20->30->

# Peek at the front element
front_element = my_queue.peek()
print(f"Front element: {front_element}")  # Output: Front element: 20

# Check if the queue is empty
is_empty = my_queue.isNull()
print(f"Is queue empty: {is_empty}")  # Output: Is queue empty: False
```

**Explanation of the Example:**

1.  **Initializing a Queue:**
    ```python
    my_queue = Queue()
    ```
    An instance of the `Queue` class is created. Since no `LinkedList` object is explicitly passed during initialization, the `Queue` constructor creates a new empty `LinkedList` to serve as the underlying storage.

2.  **Enqueueing Elements:**
    ```python
    my_queue.enqueue(10)
    my_queue.enqueue(20)
    my_queue.enqueue(30)
    ```
    The `enqueue()` method adds elements to the rear of the queue. Here, `10` is added first, then `20`, and finally `30`. The `LinkedList`'s `InsertAtEnd()` method is used for this operation.

3.  **Displaying the Queue:**
    ```python
    my_queue.display_queue()  # Output: 10->20->30->
    ```
    The `display_queue()` method calls the `display()` method of the underlying `LinkedList`, which prints the elements from the front to the rear of the queue.

4.  **Dequeueing an Element:**
    ```python
    removed_element = my_queue.dequeue()
    print(f"Removed element: {removed_element}")  # Output: Removed element: 10
    ```
    The `dequeue()` method removes and returns the element at the front of the queue (the element that was enqueued first). Here, `10` is removed. The `LinkedList`'s element at index `0` is accessed and then deleted using `deleteItem(0)`.

5.  **Displaying After Dequeue:**
    ```python
    my_queue.display_queue()  # Output: 20->30->
    ```
    After dequeueing, the `display_queue()` method shows the remaining elements in the queue, with `20` now at the front.

6.  **Peeking at the Front:**
    ```python
    front_element = my_queue.peek()
    print(f"Front element: {front_element}")  # Output: Front element: 20
    ```
    The `peek()` method returns the element at the front of the queue without removing it. Here, it returns `20`.

7.  **Checking if Empty:**
    ```python
    is_empty = my_queue.isNull()
    print(f"Is queue empty: {is_empty}")  # Output: Is queue empty: False
    ```
    The `isNull()` method checks if the queue is empty by examining its size. Since there are still elements in the queue, it returns `False`.



```

