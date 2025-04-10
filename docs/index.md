### Data structures

In this library, we implemented some important data structures and seen how they work. We have:

* **`Array_new`:** This was our custom implementation of an array. It provided a way to store a contiguous sequence of elements and likely included basic array operations like initialization and element access. We used it as one of the underlying structures for our `Stack` implementation.

* **`Node`:** This class served as the fundamental building block for our linked list and tree implementations. Each `Node` object held a `value` and references (`next` and optionally `prev` for doubly linked lists, `left` and `right` for trees) to other nodes in the data structure.

* **`LinkedList`:** This class implemented the linked list data structure, utilizing `Node` objects. It supported both singly and doubly linked lists and provided methods for inserting, deleting, accessing, searching, reversing, and updating elements within the list. We used it as the underlying structure for our `Stack` and `Queue` implementations.

* **`Stack`:** This class implemented the stack data structure, which follows the LIFO principle. It could be initialized with either an `Array_new` or a `LinkedList` object as its underlying storage. It provided methods for `push` (to add elements to the top), `pop_stack` (to remove and return the top element), `peek` (to view the top element), `isEmpty` (to check if the stack is empty), and `display_stack` (to show the stack's contents).

* **`Queue`:** This class implemented the queue data structure, following the FIFO principle. It used a `LinkedList` as its underlying storage. It provided methods for `enqueue` (to add elements to the rear), `dequeue` (to remove and return the front element), `peek` (to view the front element), `rear` (to view the rear element), `isNull` (to check if the queue is empty), and `display_queue` (to show the queue's contents).

* **`BinaryTree`:** This class inherited from the `Node` class and represented a binary tree. Each instance was a node that could have a left and a right child. It included methods for different tree traversals (`pre_order`, `in_order`, `post_order`), searching for nodes (`search_node`, `search_BST` for Binary Search Trees), and adding nodes while maintaining the BST property (`addnode`). It also had methods for building and drawing a graph representation of the tree using `networkx` and `matplotlib` (`build_graph`, `draw_graph`).

In essence, these classes provide the blueprints and functionalities for creating and manipulating different types of data structures, each designed for specific ways of organizing and accessing data.