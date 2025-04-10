```markdown
# The `Array_new` Class: A Custom Array Implementation

This document describes the `Array_new` class, which provides a custom implementation of an array-like data structure in Python, leveraging the power and efficiency of the `numpy` library as its backend.

## Class Definition

```python
import numpy as np

class Array_new:
  def __init__(self, data):
    self.data = np.array(data)
    self.shape = self.data.shape
    self.size = np.array(data).size
    self.dim = np.array(data).ndim

  def __str__(self):
    """Returns a list where all the elements are transformed to strings"""
    return f"Data = {self.data}"

  def __getitem__(self, index):
      if isinstance(index, int):
          # Handle single index subscription
          return self.data[index]
      elif isinstance(index, slice):
          # Handle slicing
          start, stop, step = index.indices(len(self))
          return Array_new(self.data[start:stop:step])  # Create a new Array_new object for the slice
      else:
          raise TypeError("Invalid index type")
  def __len__(self):
    return len(self.data)


  def max(self):
      """Returns the maximum value in the array."""
      return max(self.data)

  def min(self):
      """Returns the minimum value in the array."""
      return min(self.data)

  def sum(self):
      """Returns the sum of all elements in the array."""
      return sum(self.data)

  def show_array(self):
    print(self.data)

  def pop_array(self):
    a = self.data[-1]
    self.data = self.data[:self.__len__()-1]
    return a

  def insert(self, elt, pos = -1):
    return np.insert(np.array(self.data), pos, elt)


  def append(self, NewElt):
    self.data = np.append(self.data, NewElt)
    self.shape = self.data.shape
    self.size = self.data.size
    self.dim = self.data.ndim


  def mean(self):
      """Returns the mean (average) of the array elements."""
      return self.sum() / len(self) if len(self) else 0

  def std(self):
      """Returns the standard deviation of the array elements."""
      mean = self.mean()
      variance = sum([(x - mean) ** 2 for x in self.data]) / len(self)
      return variance ** 0.5
```

## `__init__(self, data)`

- **Purpose:** This is the constructor for the `Array_new` class. It initializes a new array object based on the input data.
- **Parameters:**
    - `data`: An iterable (like a list or tuple) containing the initial elements of the array.
- **Functionality:**
    - It converts the input `data` into a `numpy` array and stores it in the `self.data` attribute. This leverages `numpy`'s efficient array operations.
    - It calculates and stores the `shape` (dimensions of the array), `size` (total number of elements), and `dim` (number of dimensions) of the `numpy` array.

## `__str__(self)`

- **Purpose:** This special method defines how the `Array_new` object should be represented as a string.
- **Functionality:** It returns a formatted string that displays the `self.data` (the underlying `numpy` array).

## `__getitem__(self, index)`

- **Purpose:** This special method enables item access (using square brackets `[]`) for the `Array_new` object, similar to how you would access elements in a standard Python list or a `numpy` array.
- **Parameters:**
    - `index`: The index or slice specifying the element(s) to retrieve.
- **Functionality:**
    - **Integer Index:** If `index` is an integer, it returns the element at that specific position in the `self.data` array.
    - **Slice:** If `index` is a slice object, it extracts the specified portion of the `self.data` array and returns a *new* `Array_new` object containing the sliced data. This ensures that slicing an `Array_new` object results in another `Array_new` object.
    - **Invalid Type:** If `index` is of any other type, it raises a `TypeError` indicating an invalid index.

## `__len__(self)`

- **Purpose:** This special method enables the use of the `len()` function on an `Array_new` object.
- **Functionality:** It returns the number of elements in the `self.data` array.

## `max(self)`

- **Purpose:** Returns the maximum value present in the array.
- **Functionality:** It uses the built-in `max()` function on the `self.data` (the `numpy` array) to find and return the largest element.

## `min(self)`

- **Purpose:** Returns the minimum value present in the array.
- **Functionality:** It uses the built-in `min()` function on the `self.data` to find and return the smallest element.

## `sum(self)`

- **Purpose:** Returns the sum of all the elements in the array.
- **Functionality:** It uses the built-in `sum()` function on the `self.data` to calculate and return the sum of all its elements.

## `show_array(self)`

- **Purpose:** Prints the underlying `numpy` array to the console.
- **Functionality:** It uses the `print()` function to display the contents of the `self.data` attribute.

## `pop_array(self)`

- **Purpose:** Removes and returns the last element of the array, similar to the `pop()` method of a Python list.
- **Functionality:**
    - It stores the last element of `self.data` in a temporary variable `a`.
    - It then updates `self.data` to contain all elements except the last one using slicing.
    - Finally, it returns the removed element `a`.

## `insert(self, elt, pos=-1)`

- **Purpose:** Inserts a new element (`elt`) into the array at a specified position (`pos`).
- **Parameters:**
    - `elt`: The element to be inserted.
    - `pos`: The index at which the element should be inserted. A negative index counts from the end of the array (default is -1, which inserts before the last element).
- **Functionality:** It uses the `np.insert()` function from `numpy` to create a *new* `numpy` array with the element inserted at the given position. **Note:** This method returns a new `numpy` array and does not modify the `self.data` attribute in place. You would need to assign the result back to `self.data` if you want to update the array.

## `append(self, NewElt)`

- **Purpose:** Adds a new element (`NewElt`) to the end of the array, similar to the `append()` method of a Python list.
- **Parameters:**
    - `NewElt`: The element to be added to the end of the array.
- **Functionality:**
    - It uses the `np.append()` function from `numpy` to create a new `numpy` array with the `NewElt` added at the end.
    - It then updates the `self.data`, `self.shape`, `self.size`, and `self.dim` attributes of the `Array_new` object to reflect the changes.

## `mean(self)`

- **Purpose:** Calculates and returns the arithmetic mean (average) of all the elements in the array.
- **Functionality:**
    - It first calculates the sum of the array elements using `self.sum()`.
    - It then divides the sum by the number of elements (obtained using `len(self)`) to get the mean.
    - If the array is empty, it returns 0 to avoid division by zero.

## `std(self)`

- **Purpose:** Calculates and returns the standard deviation of the elements in the array. Standard deviation measures the spread or dispersion of the data around the mean.
- **Functionality:**
    - It first calculates the mean of the array using `self.mean()`.
    - It then calculates the variance by summing the squared differences between each element and the mean, and dividing by the number of elements.
    - Finally, it returns the square root of the variance, which is the standard deviation.

This `Array_new` class provides a convenient wrapper around `numpy` arrays, offering a more object-oriented interface with methods for common array operations while still benefiting from `numpy`'s performance for numerical computations.

## Example Usage of the `Array_new` Class

This section provides practical examples of how to create and interact with `Array_new` objects, demonstrating the usage of various methods defined in the class.


```python
# Create an Array_new object
my_array = Array_new([1, 2, 3, 4, 5])

# Access elements by index
print(my_array[0])  # Output: 1
print(my_array[2])  # Output: 3

# Get the shape of the array
print(my_array.shape)  # Output: (5,)

# Get the size of the array
print(my_array.size)  # Output: 5

# Get the dimension of the array
print(my_array.dim)  # Output: 1

# Get the maximum value
print(my_array.max())  # Output: 5

# Get the minimum value
print(my_array.min())  # Output: 1

# Get the sum of all elements
print(my_array.sum())  # Output: 15

# Get the mean (average)
print(my_array.mean())  # Output: 3.0

# Get the standard deviation
print(my_array.std())  # Output: 1.4142135623730951

# Display the array
my_array.show_array()

# Remove and return the last element
removed_element = my_array.pop_array()
print(f"Removed element: {removed_element}")

# Insert element at a specific position (default at the end)
inserted_array = my_array.insert(6, 2) # Note: insert returns a new numpy array
print(f"Array after insertion: {inserted_array}")

# Append new element at the end
my_array.append(7)
print(my_array)
```

**Explanation of the Example:**

1.  **Creating an `Array_new` Object:**
    ```python
    my_array = Array_new([1, 2, 3, 4, 5])
    ```
    This line creates an instance of the `Array_new` class, initializing it with a Python list `[1, 2, 3, 4, 5]`. The constructor converts this list into a `numpy` array and sets the `shape`, `size`, and `dim` attributes.

2.  **Accessing Elements by Index:**
    ```python
    print(my_array[0])  # Output: 1
    print(my_array[2])  # Output: 3
    ```
    This demonstrates the use of the `__getitem__` method to access elements at specific indices (0-based).

3.  **Getting Array Properties:**
    ```python
    print(my_array.shape)  # Output: (5,)
    print(my_array.size)   # Output: 5
    print(my_array.dim)    # Output: 1
    ```
    These lines access the `shape` (a tuple indicating the dimensions), `size` (the total number of elements), and `dim` (the number of dimensions) of the array.

4.  **Statistical Operations:**
    ```python
    print(my_array.max())   # Output: 5
    print(my_array.min())   # Output: 1
    print(my_array.sum())   # Output: 15
    print(my_array.mean())  # Output: 3.0
    print(my_array.std())   # Output: 1.4142135623730951
    ```
    These lines demonstrate the use of the `max()`, `min()`, `sum()`, `mean()`, and `std()` methods to perform basic statistical calculations on the array elements.

5.  **Displaying the Array:**
    ```python
    my_array.show_array()
    ```
    This calls the `show_array()` method, which prints the underlying `numpy` array to the console.

6.  **Removing the Last Element:**
    ```python
    removed_element = my_array.pop_array()
    print(f"Removed element: {removed_element}")
    ```
    The `pop_array()` method removes and returns the last element of the array.

7.  **Inserting an Element:**
    ```python
    inserted_array = my_array.insert(6, 2) # Note: insert returns a new numpy array
    print(f"Array after insertion: {inserted_array}")
    ```
    The `insert()` method inserts the value `6` at index `2`. **Important:** As noted in the code comment, the `insert()` method from `numpy` returns a *new* `numpy` array. The original `my_array` object's `data` attribute is not modified in place by this implementation.

8.  **Appending an Element:**
    ```python
    my_array.append(7)
    print(my_array)
    ```
    The `append()` method adds the value `7` to the end of the array. This method *does* modify the `self.data` attribute of the `my_array` object in place and updates its `shape`, `size`, and `dim`.

This example provides a clear illustration of how to use the `Array_new` class for common array operations. Pay close attention to the behavior of the `insert()` method, which returns a new array rather than modifying the original in place.
```