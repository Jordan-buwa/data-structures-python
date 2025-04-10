```markdown
# The  `BinaryTree` Class for Binary Tree Implementation


The `Node` class provides the basic structure for a tree node with a value and references to left and right children, along with methods for building and drawing a graph representation.

## `BinaryTree` Class

The `BinaryTree` class inherits from the `Node` class and provides specific methods for binary tree operations, such as different types of traversals (pre-order, in-order, post-order) and searching for nodes.

```python 
class BinaryTree(Node):
  def __init__(self, value = None, l = None, r = None):
    self.root = self
    Node.__init__(self, value, l, r)

  def __str__(self) -> str:
    return str(self.value)

  def pre_order(self):
    if not self:
      return
    tem = self.root
    print(tem.value)
    if tem.left:
      tem.left.pre_order()
    if tem.right:
      tem.right.pre_order()
  def in_order(self):
    if not self:
      return
    tem = self.root
    if tem.left:
      tem.left.in_order()
    print(tem.value)
    if tem.right:
      tem.right.in_order()

  def post_order(self):
    if not self:
      return
    tem = self.root
    if tem.left:
      tem.left.post_order()
    if tem.right:
      tem.right.post_order()
    print(tem.value)

  def search_node(self, target):
    if not self.root:
      return False
    if self.value == target:
      return True
    # Calling search_node on children.
    if self.left and self.left.search_node(target):
      return True
    if self.right and self.right.search_node(target):
      return True
    return False

  def search_BST(self, target):
    if not self.root:
      return False
    if self.value == target:
      return True
    if target < self.value and self.left: return self.left.search_BST(target)
    elif target >= self.value and self.right: return self.right.search_BST(target)
    return False

  def addnode(self, data):
    newNode = BinaryTree(data)
    if self.root is None:
      self.root = newNode
      return

    current = self.root
    while True:
      if data < current.value:
        if current.left is None:
          current.left = newNode
          return
        current = current.left
      else:
        if current.right is None:
          current.right = newNode
          return
        current = current.right


def delete_node_bst(root, key):

  def find_min(node):
    current = node
    while current.left is not None:
      current = current.left
    return current

  def find_max(node):
    current = node
    while current.right is not None:
      current = current.right
    return current

    if not root:
      return root

  if key < root.value:
      root.left = delete_node_bst(root.left, key)
  elif key > root.value:
      root.right = delete_node_bst(root.right, key)
  else:  # Key is equal to root's data (node to be deleted)
      # Case 1: Leaf node
      if root.left is None and root.right is None:
          root = None
      # Case 2: Node with one child
      elif root.left is None:
          root = root.right
      elif root.right is None:
          root = root.left
      # Case 3: Node with two children
      else:
          # Find the inorder successor (smallest in the right subtree)
          successor = find_min(root.right)
          # Replace the current node's data with the successor's data
          root.value = successor.value
          # Delete the successor from the right subtree
          root.right = delete_node_bst(root.right, successor.value)

  return root
```

### `__init__(self, value=None, l=None, r=None)`

- **Purpose:** This is the constructor for the `BinaryTree` class. It initializes a new binary tree node.
- **Parameters:**
    - `value`: The data to be stored in this node. Defaults to `None`.
    - `l`: An optional reference to the left child node. Defaults to `None`.
    - `r`: An optional reference to the right child node. Defaults to `None`.
- **Functionality:** It calls the `__init__` of the parent `Node` class to initialize the `value`, `left`, and `right` attributes. It also sets `self.root` to `self`, making the current instance the root of the (sub)tree.

### `__str__(self) -> str`

- **Purpose:** Defines how the `BinaryTree` object should be represented as a string.
- **Functionality:** It returns the string representation of the node's `value`.

### `pre_order(self)`

- **Purpose:** Performs a pre-order traversal of the binary tree (Root -> Left -> Right).
- **Functionality:**
    - If the current node is not `None`, it prints the node's `value`.
    - Then, it recursively calls `pre_order` on the left child.
    - Finally, it recursively calls `pre_order` on the right child.

### `in_order(self)`

- **Purpose:** Performs an in-order traversal of the binary tree (Left -> Root -> Right).
- **Functionality:**
    - If the current node is not `None`, it recursively calls `in_order` on the left child.
    - Then, it prints the node's `value`.
    - Finally, it recursively calls `in_order` on the right child.

### `post_order(self)`

- **Purpose:** Performs a post-order traversal of the binary tree (Left -> Right -> Root).
- **Functionality:**
    - If the current node is not `None`, it recursively calls `post_order` on the left child.
    - Then, it recursively calls `post_order` on the right child.
    - Finally, it prints the node's `value`.

### `search_node(self, target)`

- **Purpose:** Searches for a node with a specific `target` value in the binary tree.
- **Parameters:**
    - `target`: The value to search for.
- **Functionality:**
    - If the current node (or root) is `None`, it returns `False`.
    - If the current node's `value` matches the `target`, it returns `True`.
    - Otherwise, it recursively calls `search_node` on the left and right children. If either of these calls returns `True`, the method returns `True`.
    - If the `target` is not found in the current node or its subtrees, it returns `False`.

### `search_BST(self, target)`

- **Purpose:** Searches for a `target` value in a Binary Search Tree (BST). This method assumes the tree follows the BST property (left child's value is less than the parent, right child's value is greater than or equal to the parent).
- **Parameters:**
    - `target`: The value to search for.
- **Functionality:**
    - If the current node (or root) is `None`, it returns `False`.
    - If the current node's `value` matches the `target`, it returns `True`.
    - If the `target` is less than the current node's `value` and the left child exists, it recursively calls `search_BST` on the left child.
    - If the `target` is greater than or equal to the current node's `value` and the right child exists, it recursively calls `search_BST` on the right child.
    - If the `target` is not found based on these comparisons, it returns `False`.

### `addnode(self, data)`

- **Purpose:** Adds a new node with the given `data` to the Binary Search Tree (BST), maintaining the BST property.
- **Parameters:**
    - `data`: The value to be inserted into the BST.
- **Functionality:**
    - It creates a new `BinaryTree` node with the given `data`.
    - If the tree is empty (root is `None`), the new node becomes the root.
    - Otherwise, it starts from the root and traverses down the tree.
    - If `data` is less than the current node's `value`, it moves to the left child. If the left child is `None`, the new node is inserted as the left child.
    - If `data` is greater than or equal to the current node's `value`, it moves to the right child. If the right child is `None`, the new node is inserted as the right child.
    - This process continues until an appropriate empty position is found for the new node.

## `delete_node_bst(root, key)` (Function)

- **Purpose:** Deletes a node with a specific `key` from a Binary Search Tree (BST), maintaining the BST property. This is a standalone function, not a method of the `BinaryTree` class.
- **Parameters:**
    - `root`: The root node of the BST.
    - `key`: The value of the node to be deleted.
- **Functionality:**
    - It includes helper functions `find_min` (to find the minimum value in a subtree) and `find_max` (to find the maximum value in a subtree), although `find_max` is not used in this specific implementation.
    - If the `root` is `None`, it returns `None`.
    - If the `key` is less than the `root`'s `value`, it recursively calls `delete_node_bst` on the left subtree.
    - If the `key` is greater than the `root`'s `value`, it recursively calls `delete_node_bst` on the right subtree.
    - If the `key` is equal to the `root`'s `value` (the node to be deleted):
        - **Case 1: Leaf node:** If the node has no children, it is simply set to `None`.
        - **Case 2: Node with one child:** If the node has only a left or a right child, it is replaced by its child.
        - **Case 3: Node with two children:**
            - It finds the inorder successor (the smallest node in the right subtree) using `find_min`.
            - It replaces the current node's `value` with the `value` of the successor.
            - It then recursively deletes the successor from the right subtree.
    - Finally, it returns the modified `root` of the subtree.


## Example Usage of the `BinaryTree` Class


```python
# Creating a Binary Search Tree and adding nodes
a = BinaryTree(8)
a.left = BinaryTree(3)
a.right = BinaryTree(10)
a.left.left = BinaryTree(1)
a.left.right = BinaryTree(6)
a.left.right.right = BinaryTree(7)
a.left.right.left = BinaryTree(4)
a.right.right = BinaryTree(14)
a.right.right.left = BinaryTree(13)
a.addnode(9)
a.addnode(20)
a.addnode(2)

# Drawing the graph of the BST
a.draw_graph()

# Searching for a node in the BST
print(f"Search for 20 in BST: {a.search_BST(20)}")

print("\n--- Example BST Deletion ---")
# Example BST for deletion
root = BinaryTree(50)
root.left = BinaryTree(30)
root.right = BinaryTree(70)
root.left.left = BinaryTree(20)
root.left.right = BinaryTree(40)
root.right.left = BinaryTree(60)
root.right.right = BinaryTree(80)

print("\nPre-order traversal of the initial BST:")
root.pre_order()
root.draw_graph()

# Delete a leaf node (20)
root = delete_node_bst(root, 20)
print("\nAfter deleting 20 (pre-order):")
root.pre_order()
root.draw_graph()

# Delete a node with one child (30)
root = delete_node_bst(root, 30)
print("\nAfter deleting 30 (pre-order):")
root.pre_order()
root.draw_graph()

# Delete a node with two children (50)
root = delete_node_bst(root, 50)
print("\nAfter deleting 50 (pre-order):")
root.pre_order()
root.draw_graph()
```

**Explanation of the Example:**

1.  **Creating a Binary Search Tree and Adding Nodes:**
    - An initial binary tree structure is created.
    - The `addnode()` method is then used to insert new nodes (`9`, `20`, `2`) into the tree while maintaining the Binary Search Tree (BST) property. The `addnode` method ensures that smaller values are inserted to the left and larger values to the right.

2.  **Drawing the Graph:**
    - `a.draw_graph()` visualizes the constructed BST using `networkx` and `matplotlib`.

3.  **Searching in the BST:**
    - `a.search_BST(20)` demonstrates how to search for a specific value (`20`) in the BST. The output `True` confirms that the node with the value `20` exists in the tree.

4.  **BST Deletion Example:**
    - A new BST is created for demonstrating the `delete_node_bst` function.
    - **Pre-order Traversal:** The `pre_order()` method is called to print the initial structure of the BST (Root -> Left -> Right).
    - **Deleting a Leaf Node (20):** The `delete_node_bst(root, 20)` function is called to remove the leaf node with the value `20`. The subsequent pre-order traversal and graph drawing show the tree after deletion.
    - **Deleting a Node with One Child (30):** `delete_node_bst(root, 30)` removes the node with value `30`, which has one child (`40`). The node is replaced by its child. The pre-order traversal and graph drawing reflect this change.
    - **Deleting a Node with Two Children (50):** `delete_node_bst(root, 50)` removes the root node, which has two children. The inorder successor (the smallest node in the right subtree, which is `60`) replaces the root, and the successor is then deleted from its original position. The final pre-order traversal and graph drawing illustrate the BST after this deletion.

This example showcases the fundamental operations on a Binary Search Tree, including insertion (using `addnode`), searching (`search_BST`), traversal (`pre_order`), visualization (`draw_graph`), and deletion (`delete_node_bst`), highlighting how these operations maintain the BST properties where applicable.








```