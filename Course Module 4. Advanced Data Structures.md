---
tags: [DSA Java]
title: Course Module 4. Advanced Data Structures
created: '2024-09-17T13:58:23.195Z'
modified: '2024-09-17T14:32:22.239Z'
---

# **Course Module 4. Advanced Data Structures**

**Duration:** 2 Weeks

In this module, we delve deeper into more sophisticated data structures that are pivotal for solving complex algorithmic problems. Advanced data structures like heaps, graphs, balanced search trees, tries, and union-find structures not only optimize performance but also enable the handling of intricate problem scenarios commonly encountered in technical interviews at top-tier companies like Microsoft and Google. This module is designed to build upon your foundational knowledge, ensuring that even those from non-IT backgrounds can grasp and apply these concepts effectively.

---

## **Week 1: Heaps, Priority Queues, and Graphs**

### **1. Heaps and Priority Queues**

#### **1.1 Min-Heap and Max-Heap Implementation**

**Overview:**
Heaps are specialized tree-based data structures that satisfy the heap property. A **Min-Heap** ensures that the parent node is less than or equal to its child nodes, making the smallest element accessible at the root. Conversely, a **Max-Heap** ensures that the parent node is greater than or equal to its child nodes, allowing quick access to the largest element.

**Topics Covered:**
- **Heap Structure and Properties**
- **Array Representation of Heaps**
- **Insertion and Deletion Operations**
- **Heapify Process**

**Detailed Explanation:**

**Heap Structure:**
A heap is a complete binary tree, meaning all levels are fully filled except possibly the last, which is filled from left to right. This property allows heaps to be efficiently represented using arrays.

**Array Representation:**
In an array-based heap:
- The parent of the node at index `i` is at index `(i-1)/2`.
- The left child is at index `2i + 1`.
- The right child is at index `2i + 2`.

**Implementation in Java:**

```java
import java.util.ArrayList;

class MinHeap {
    private ArrayList<Integer> heap;

    public MinHeap() {
        heap = new ArrayList<>();
    }

    // Insert a new element into the heap
    public void insert(int val) {
        heap.add(val);
        heapifyUp(heap.size() - 1);
    }

    // Remove and return the minimum element
    public int extractMin() {
        if (heap.size() == 0) throw new IllegalStateException("Heap is empty");
        if (heap.size() == 1) return heap.remove(0);
        int min = heap.get(0);
        heap.set(0, heap.remove(heap.size() - 1));
        heapifyDown(0);
        return min;
    }

    // Heapify up to maintain heap property after insertion
    private void heapifyUp(int index) {
        int parent = (index - 1) / 2;
        if (index > 0 && heap.get(index) < heap.get(parent)) {
            swap(index, parent);
            heapifyUp(parent);
        }
    }

    // Heapify down to maintain heap property after extraction
    private void heapifyDown(int index) {
        int smallest = index;
        int left = 2 * index + 1;
        int right = 2 * index + 2;

        if (left < heap.size() && heap.get(left) < heap.get(smallest)) {
            smallest = left;
        }

        if (right < heap.size() && heap.get(right) < heap.get(smallest)) {
            smallest = right;
        }

        if (smallest != index) {
            swap(index, smallest);
            heapifyDown(smallest);
        }
    }

    // Utility method to swap elements in the heap
    private void swap(int i, int j) {
        int temp = heap.get(i);
        heap.set(i, heap.get(j));
        heap.set(j, temp);
    }

    // Check if the heap is empty
    public boolean isEmpty() {
        return heap.isEmpty();
    }

    // Get the size of the heap
    public int size() {
        return heap.size();
    }

    // Peek at the minimum element without removing it
    public int peek() {
        if (heap.size() == 0) throw new IllegalStateException("Heap is empty");
        return heap.get(0);
    }
}

class MaxHeap {
    private ArrayList<Integer> heap;

    public MaxHeap() {
        heap = new ArrayList<>();
    }

    // Insert a new element into the heap
    public void insert(int val) {
        heap.add(val);
        heapifyUp(heap.size() - 1);
    }

    // Remove and return the maximum element
    public int extractMax() {
        if (heap.size() == 0) throw new IllegalStateException("Heap is empty");
        if (heap.size() == 1) return heap.remove(0);
        int max = heap.get(0);
        heap.set(0, heap.remove(heap.size() - 1));
        heapifyDown(0);
        return max;
    }

    // Heapify up to maintain heap property after insertion
    private void heapifyUp(int index) {
        int parent = (index - 1) / 2;
        if (index > 0 && heap.get(index) > heap.get(parent)) {
            swap(index, parent);
            heapifyUp(parent);
        }
    }

    // Heapify down to maintain heap property after extraction
    private void heapifyDown(int index) {
        int largest = index;
        int left = 2 * index + 1;
        int right = 2 * index + 2;

        if (left < heap.size() && heap.get(left) > heap.get(largest)) {
            largest = left;
        }

        if (right < heap.size() && heap.get(right) > heap.get(largest)) {
            largest = right;
        }

        if (largest != index) {
            swap(index, largest);
            heapifyDown(largest);
        }
    }

    // Utility method to swap elements in the heap
    private void swap(int i, int j) {
        int temp = heap.get(i);
        heap.set(i, heap.get(j));
        heap.set(j, temp);
    }

    // Check if the heap is empty
    public boolean isEmpty() {
        return heap.isEmpty();
    }

    // Get the size of the heap
    public int size() {
        return heap.size();
    }

    // Peek at the maximum element without removing it
    public int peek() {
        if (heap.size() == 0) throw new IllegalStateException("Heap is empty");
        return heap.get(0);
    }
}
```

**Explanation:**
- **MinHeap and MaxHeap Classes:** Both classes use an `ArrayList` to store heap elements. The primary difference lies in the `heapifyUp` and `heapifyDown` methods, which enforce the min-heap and max-heap properties, respectively.
- **Insertion (`insert`):** Adds the new element to the end of the array and then heapifies up to maintain the heap property.
- **Extraction (`extractMin` / `extractMax`):** Removes the root element (minimum or maximum), replaces it with the last element, and then heapifies down to restore the heap property.
- **Heapify Methods:** Ensure that the heap property is maintained after insertion or extraction by swapping elements as necessary.

#### **1.2 Heap Sort Algorithm**

**Overview:**
Heap Sort is a comparison-based sorting algorithm that leverages the heap data structure to sort elements efficiently. It has a time complexity of O(n log n) and is particularly useful for large datasets.

**Topics Covered:**
- **Building a Heap from an Array**
- **Extracting Elements to Sort**
- **In-Place Heap Sort Implementation**

**Detailed Explanation:**

**Heap Sort Process:**
1. **Build a Max-Heap:** Transform the unsorted array into a max-heap, where the largest element is at the root.
2. **Extract the Maximum Element:** Swap the root with the last element in the heap and reduce the heap size by one.
3. **Heapify the Root:** Restore the max-heap property by heapifying the new root element.
4. **Repeat:** Continue the extraction and heapify steps until the heap size is reduced to one.

**Implementation in Java:**

```java
public class HeapSort {
    // Function to perform heap sort
    public static void heapSort(int[] arr) {
        int n = arr.length;

        // Build max heap
        for (int i = n / 2 - 1; i >= 0; i--)
            heapify(arr, n, i);

        // Extract elements from heap one by one
        for (int i = n - 1; i >= 0; i--) {
            // Move current root to end
            swap(arr, 0, i);

            // Call heapify on the reduced heap
            heapify(arr, i, 0);
        }
    }

    // To heapify a subtree rooted at index i
    private static void heapify(int[] arr, int n, int i) {
        int largest = i;       // Initialize largest as root
        int left = 2 * i + 1;  // left child
        int right = 2 * i + 2; // right child

        // If left child is larger than root
        if (left < n && arr[left] > arr[largest])
            largest = left;

        // If right child is larger than largest so far
        if (right < n && arr[right] > arr[largest])
            largest = right;

        // If largest is not root
        if (largest != i) {
            swap(arr, i, largest);

            // Recursively heapify the affected sub-tree
            heapify(arr, n, largest);
        }
    }

    // Utility method to swap elements in the array
    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // Utility method to print the array
    public static void printArray(int[] arr) {
        for (int num : arr)
            System.out.print(num + " ");
        System.out.println();
    }

    // Example usage
    public static void main(String[] args) {
        int[] arr = {12, 11, 13, 5, 6, 7};
        System.out.println("Original array:");
        printArray(arr);

        heapSort(arr);

        System.out.println("Sorted array:");
        printArray(arr);
    }
}
```

**Explanation:**
- **Building the Heap:** The initial loop constructs a max-heap from the unsorted array by calling `heapify` on all non-leaf nodes starting from the bottom.
- **Sorting Process:** After building the max-heap, the largest element (root) is swapped with the last element. The heap size is reduced, and `heapify` is called on the new root to maintain the heap property. This process is repeated until the entire array is sorted.
- **In-Place Sorting:** Heap Sort sorts the array in place without requiring additional memory, making it space-efficient.

**Output:**
```
Original array:
12 11 13 5 6 7 
Sorted array:
5 6 7 11 12 13 
```

**Advantages of Heap Sort:**
- **Time Efficiency:** O(n log n) time complexity.
- **Space Efficiency:** In-place sorting with O(1) auxiliary space.
- **No Worst-Case Degradation:** Consistent performance regardless of input data.

#### **1.3 Priority Queues**

**Overview:**
A priority queue is an abstract data type where each element has a priority. Elements are dequeued based on their priority rather than their insertion order. Heaps are commonly used to implement priority queues due to their efficient retrieval of the highest (or lowest) priority element.

**Topics Covered:**
- **Priority Queue Operations**
- **Applications of Priority Queues**
- **Implementation Using Heaps**

**Detailed Explanation:**

**Priority Queue Operations:**
- **Insert (enqueue):** Add an element with an associated priority.
- **Extract-Min / Extract-Max (dequeue):** Remove and return the element with the highest or lowest priority.
- **Peek:** View the element with the highest or lowest priority without removing it.
- **Increase/Decrease Key:** Modify the priority of an existing element.

**Applications:**
- **Dijkstra’s Shortest Path Algorithm:** Determines the shortest path in a graph.
- **Huffman Coding:** Used for data compression.
- **Task Scheduling:** Prioritizing tasks based on urgency.

**Implementation Using Heaps:**
Priority queues can be efficiently implemented using min-heaps or max-heaps, where the heap property ensures that the highest or lowest priority element is always accessible at the root.

**Example: Implementing a Priority Queue Using MinHeap**

```java
public class PriorityQueueExample {
    public static void main(String[] args) {
        MinHeap pq = new MinHeap();

        // Insert elements with priorities
        pq.insert(10);
        pq.insert(5);
        pq.insert(20);
        pq.insert(1);

        System.out.println("Priority Queue (Min-Heap):");
        while (!pq.isEmpty()) {
            System.out.print(pq.extractMin() + " ");
        }
        // Output: 1 5 10 20
    }
}
```

**Explanation:**
- **Insertion:** Elements are inserted into the min-heap, maintaining the heap property.
- **Extraction:** The `extractMin` method removes and returns the smallest element, effectively dequeuing the highest priority element.

---

### **2. Graphs**

#### **2.1 Graph Representations (Adjacency Matrix, List)**

**Overview:**
Graphs are fundamental data structures used to model relationships between objects. They consist of vertices (nodes) connected by edges. Efficient graph representation is crucial for performing various graph algorithms effectively.

**Topics Covered:**
- **Graph Terminology:** Vertices, Edges, Directed vs. Undirected, Weighted vs. Unweighted.
- **Adjacency Matrix Representation**
- **Adjacency List Representation**
- **Choosing the Right Representation**

**Detailed Explanation:**

**Graph Terminology:**
- **Vertices (Nodes):** Fundamental units representing entities.
- **Edges (Links):** Connections between vertices.
- **Directed Graph:** Edges have a direction (from one vertex to another).
- **Undirected Graph:** Edges have no direction.
- **Weighted Graph:** Edges have associated weights or costs.
- **Unweighted Graph:** Edges have no weights.

**Adjacency Matrix:**
A 2D array where the cell at `[i][j]` indicates the presence (and possibly the weight) of an edge between vertex `i` and vertex `j`.

**Advantages:**
- **Constant-time edge checks:** O(1) time to check if an edge exists.
- **Simple implementation.**

**Disadvantages:**
- **Space Inefficiency:** Requires O(V²) space, where V is the number of vertices.
- **Inefficient for sparse graphs.**

**Implementation in Java:**

```java
class GraphAdjacencyMatrix {
    private int[][] adjMatrix;
    private int numVertices;

    public GraphAdjacencyMatrix(int numVertices) {
        this.numVertices = numVertices;
        adjMatrix = new int[numVertices][numVertices];
    }

    // Add edge (undirected)
    public void addEdge(int i, int j) {
        adjMatrix[i][j] = 1;
        adjMatrix[j][i] = 1;
    }

    // Remove edge
    public void removeEdge(int i, int j) {
        adjMatrix[i][j] = 0;
        adjMatrix[j][i] = 0;
    }

    // Check if edge exists
    public boolean hasEdge(int i, int j) {
        return adjMatrix[i][j] == 1;
    }

    // Display the adjacency matrix
    public void display() {
        for (int i = 0; i < numVertices; i++) {
            for (int j = 0; j < numVertices; j++) {
                System.out.print(adjMatrix[i][j] + " ");
            }
            System.out.println();
        }
    }

    // Example usage
    public static void main(String[] args) {
        GraphAdjacencyMatrix graph = new GraphAdjacencyMatrix(4);
        graph.addEdge(0, 1);
        graph.addEdge(0, 2);
        graph.addEdge(1, 2);
        graph.addEdge(2, 3);
        graph.display();
        /*
        Output:
        0 1 1 0 
        1 0 1 0 
        1 1 0 1 
        0 0 1 0 
        */
    }
}
```

**Adjacency List:**
An array of lists where each list corresponds to a vertex and contains its adjacent vertices.

**Advantages:**
- **Space Efficiency:** Requires O(V + E) space, where E is the number of edges.
- **Efficient for Sparse Graphs.**

**Disadvantages:**
- **Edge Checks are Slower:** O(V) time in the worst case to check if an edge exists.
- **More Complex Implementation Compared to Adjacency Matrix.**

**Implementation in Java:**

```java
import java.util.LinkedList;

class GraphAdjacencyList {
    private LinkedList<Integer>[] adjList;
    private int numVertices;

    @SuppressWarnings("unchecked")
    public GraphAdjacencyList(int numVertices) {
        this.numVertices = numVertices;
        adjList = new LinkedList[numVertices];
        for(int i = 0; i < numVertices; i++) {
            adjList[i] = new LinkedList<>();
        }
    }

    // Add edge (undirected)
    public void addEdge(int i, int j) {
        adjList[i].add(j);
        adjList[j].add(i);
    }

    // Remove edge
    public void removeEdge(int i, int j) {
        adjList[i].remove(Integer.valueOf(j));
        adjList[j].remove(Integer.valueOf(i));
    }

    // Check if edge exists
    public boolean hasEdge(int i, int j) {
        return adjList[i].contains(j);
    }

    // Display the adjacency list
    public void display() {
        for(int i = 0; i < numVertices; i++) {
            System.out.print("Vertex " + i + ": ");
            for(int vertex : adjList[i]) {
                System.out.print(vertex + " ");
            }
            System.out.println();
        }
    }

    // Example usage
    public static void main(String[] args) {
        GraphAdjacencyList graph = new GraphAdjacencyList(4);
        graph.addEdge(0, 1);
        graph.addEdge(0, 2);
        graph.addEdge(1, 2);
        graph.addEdge(2, 3);
        graph.display();
        /*
        Output:
        Vertex 0: 1 2 
        Vertex 1: 0 2 
        Vertex 2: 0 1 3 
        Vertex 3: 2 
        */
    }
}
```

**Choosing the Right Representation:**
- **Adjacency Matrix:** Suitable for dense graphs where E is close to V².
- **Adjacency List:** Ideal for sparse graphs with significantly fewer edges.

#### **2.2 Weighted and Unweighted Graphs**

**Overview:**
Graphs can be categorized based on whether their edges carry weights or not. **Weighted Graphs** assign a value (weight) to each edge, representing cost, distance, or capacity. **Unweighted Graphs** treat all edges equally without any associated weight.

**Topics Covered:**
- **Definition and Examples of Weighted and Unweighted Graphs**
- **Applications of Weighted Graphs**
- **Modifying Graph Representations to Handle Weights**

**Detailed Explanation:**

**Unweighted Graphs:**
In unweighted graphs, edges signify a connection without any additional information.

**Weighted Graphs:**
Each edge has an associated weight, which can represent various metrics depending on the application.

**Applications of Weighted Graphs:**
- **Shortest Path Problems:** Finding the least cost path between nodes.
- **Minimum Spanning Trees:** Connecting all nodes with the minimum total edge weight.
- **Network Routing:** Determining optimal paths in communication networks.

**Modifying Graph Representations:**

**Weighted Adjacency Matrix:**
Instead of using `1` to represent the presence of an edge, use the actual weight. If no edge exists, use a sentinel value like `0` or `Infinity`.

**Implementation in Java:**

```java
class WeightedGraphAdjacencyMatrix {
    private int[][] adjMatrix;
    private int numVertices;
    private final int INF = Integer.MAX_VALUE;

    public WeightedGraphAdjacencyMatrix(int numVertices) {
        this.numVertices = numVertices;
        adjMatrix = new int[numVertices][numVertices];
        // Initialize all edges to INF (no connection)
        for(int i = 0; i < numVertices; i++) {
            for(int j = 0; j < numVertices; j++) {
                if(i == j)
                    adjMatrix[i][j] = 0;
                else
                    adjMatrix[i][j] = INF;
            }
        }
    }

    // Add edge with weight
    public void addEdge(int i, int j, int weight) {
        adjMatrix[i][j] = weight;
        adjMatrix[j][i] = weight; // For undirected graph
    }

    // Remove edge
    public void removeEdge(int i, int j) {
        adjMatrix[i][j] = INF;
        adjMatrix[j][i] = INF;
    }

    // Get weight of edge
    public int getWeight(int i, int j) {
        return adjMatrix[i][j];
    }

    // Display the adjacency matrix
    public void display() {
        for(int i = 0; i < numVertices; i++) {
            for(int j = 0; j < numVertices; j++) {
                if(adjMatrix[i][j] == INF)
                    System.out.print("INF ");
                else
                    System.out.print(adjMatrix[i][j] + " ");
            }
            System.out.println();
        }
    }

    // Example usage
    public static void main(String[] args) {
        WeightedGraphAdjacencyMatrix graph = new WeightedGraphAdjacencyMatrix(4);
        graph.addEdge(0, 1, 5);
        graph.addEdge(0, 2, 3);
        graph.addEdge(1, 2, 2);
        graph.addEdge(2, 3, 4);
        graph.display();
        /*
        Output:
        0 5 3 INF 
        5 0 2 INF 
        3 2 0 4 
        INF INF 4 0 
        */
    }
}
```

**Weighted Adjacency List:**
Each entry in the adjacency list stores both the adjacent vertex and the weight of the connecting edge.

**Implementation in Java:**

```java
import java.util.LinkedList;

class WeightedGraphAdjacencyList {
    private LinkedList<Edge>[] adjList;
    private int numVertices;

    // Edge class to store destination and weight
    static class Edge {
        int dest;
        int weight;

        Edge(int dest, int weight) {
            this.dest = dest;
            this.weight = weight;
        }
    }

    @SuppressWarnings("unchecked")
    public WeightedGraphAdjacencyList(int numVertices) {
        this.numVertices = numVertices;
        adjList = new LinkedList[numVertices];
        for(int i = 0; i < numVertices; i++) {
            adjList[i] = new LinkedList<>();
        }
    }

    // Add edge with weight (undirected)
    public void addEdge(int src, int dest, int weight) {
        adjList[src].add(new Edge(dest, weight));
        adjList[dest].add(new Edge(src, weight));
    }

    // Remove edge
    public void removeEdge(int src, int dest) {
        adjList[src].removeIf(edge -> edge.dest == dest);
        adjList[dest].removeIf(edge -> edge.dest == src);
    }

    // Get edges of a vertex
    public LinkedList<Edge> getEdges(int vertex) {
        return adjList[vertex];
    }

    // Display the adjacency list
    public void display() {
        for(int i = 0; i < numVertices; i++) {
            System.out.print("Vertex " + i + ": ");
            for(Edge edge : adjList[i]) {
                System.out.print(" -> " + edge.dest + "(" + edge.weight + ")");
            }
            System.out.println();
        }
    }

    // Example usage
    public static void main(String[] args) {
        WeightedGraphAdjacencyList graph = new WeightedGraphAdjacencyList(4);
        graph.addEdge(0, 1, 5);
        graph.addEdge(0, 2, 3);
        graph.addEdge(1, 2, 2);
        graph.addEdge(2, 3, 4);
        graph.display();
        /*
        Output:
        Vertex 0:  -> 1(5) -> 2(3)
        Vertex 1:  -> 0(5) -> 2(2)
        Vertex 2:  -> 0(3) -> 1(2) -> 3(4)
        Vertex 3:  -> 2(4)
        */
    }
}
```

**Explanation:**
- **Edge Class:** Represents an edge with a destination vertex and a weight.
- **Adjacency List:** Each vertex's list contains `Edge` objects, storing connected vertices and their corresponding weights.
- **Advantages:**
  - **Space Efficiency:** Especially beneficial for sparse graphs.
  - **Flexibility:** Easily accommodates varying edge weights.

---

## **Week 2: Balanced Search Trees, Tries, and Union-Find Structures**

### **3. Balanced Search Trees**

#### **3.1 AVL Trees**

**Overview:**
An **AVL (Adelson-Velsky and Landis) Tree** is a self-balancing binary search tree (BST) where the difference in heights between the left and right subtrees (balance factor) of any node is at most one. This balancing ensures that the tree maintains O(log n) time complexity for insertion, deletion, and search operations.

**Topics Covered:**
- **AVL Tree Properties**
- **Rotations (Single and Double)**
- **Insertion and Deletion in AVL Trees**
- **Maintaining Balance**

**Detailed Explanation:**

**AVL Tree Properties:**
- **Balance Factor:** For any node, the height difference between its left and right subtrees is -1, 0, or +1.
- **Self-Balancing:** Automatically adjusts its structure through rotations to maintain balance after insertions and deletions.

**Rotations:**
To restore balance, AVL trees perform rotations:
- **Left Rotation**
- **Right Rotation**
- **Left-Right Rotation**
- **Right-Left Rotation**

**Implementation in Java:**

```java
class AVLTree {
    class Node {
        int key, height;
        Node left, right;

        Node(int d) {
            key = d;
            height = 1;
        }
    }

    private Node root;

    // Get height of the node
    private int height(Node N) {
        if (N == null)
            return 0;
        return N.height;
    }

    // Get balance factor of node N
    private int getBalance(Node N) {
        if (N == null)
            return 0;
        return height(N.left) - height(N.right);
    }

    // Right rotate subtree rooted with y
    private Node rightRotate(Node y) {
        Node x = y.left;
        Node T2 = x.right;

        // Perform rotation
        x.right = y;
        y.left = T2;

        // Update heights
        y.height = Math.max(height(y.left), height(y.right)) + 1;
        x.height = Math.max(height(x.left), height(x.right)) + 1;

        // Return new root
        return x;
    }

    // Left rotate subtree rooted with x
    private Node leftRotate(Node x) {
        Node y = x.right;
        Node T2 = y.left;

        // Perform rotation
        y.left = x;
        x.right = T2;

        // Update heights
        x.height = Math.max(height(x.left), height(x.right)) + 1;
        y.height = Math.max(height(y.left), height(y.right)) + 1;

        // Return new root
        return y;
    }

    // Insert a key into the AVL tree
    public void insert(int key) {
        root = insertRec(root, key);
    }

    private Node insertRec(Node node, int key) {
        // Perform normal BST insertion
        if (node == null)
            return new Node(key);
        if (key < node.key)
            node.left = insertRec(node.left, key);
        else if (key > node.key)
            node.right = insertRec(node.right, key);
        else // Duplicate keys not allowed
            return node;

        // Update height of this ancestor node
        node.height = 1 + Math.max(height(node.left), height(node.right));

        // Get balance factor to check whether this node became unbalanced
        int balance = getBalance(node);

        // If node is unbalanced, then there are 4 cases

        // Left Left Case
        if (balance > 1 && key < node.left.key)
            return rightRotate(node);

        // Right Right Case
        if (balance < -1 && key > node.right.key)
            return leftRotate(node);

        // Left Right Case
        if (balance > 1 && key > node.left.key) {
            node.left = leftRotate(node.left);
            return rightRotate(node);
        }

        // Right Left Case
        if (balance < -1 && key < node.right.key) {
            node.right = rightRotate(node.right);
            return leftRotate(node);
        }

        // Return the unchanged node pointer
        return node;
    }

    // Preorder traversal of the tree
    public void preOrder() {
        preOrderRec(root);
        System.out.println();
    }

    private void preOrderRec(Node node) {
        if (node != null) {
            System.out.print(node.key + " ");
            preOrderRec(node.left);
            preOrderRec(node.right);
        }
    }

    // Example usage
    public static void main(String[] args) {
        AVLTree tree = new AVLTree();

        /* Constructing tree given in the example */
        tree.insert(10);
        tree.insert(20);
        tree.insert(30);
        tree.insert(40);
        tree.insert(50);
        tree.insert(25);

        /* The constructed AVL Tree would be
                30
               /  \
             20   40
            /  \     \
          10  25    50
        */

        System.out.println("Preorder traversal of constructed AVL tree is:");
        tree.preOrder();
        // Output: 30 20 10 25 40 50 
    }
}
```

**Explanation:**
- **Node Class:** Represents each node in the AVL tree, storing the key, height, and references to left and right children.
- **Insertion (`insert`):** Inserts a key using standard BST insertion. After insertion, updates the height and checks the balance factor to determine if rotations are needed.
- **Rotations:** Based on the balance factor and the nature of the imbalance, performs appropriate rotations to restore balance.
- **Preorder Traversal:** Visits nodes in the order: root, left subtree, right subtree, useful for verifying the structure of the AVL tree.

**Advantages of AVL Trees:**
- **Strict Balancing:** Guarantees O(log n) time complexity for search, insert, and delete operations.
- **Efficient for Read-Heavy Operations:** Ideal when search operations are more frequent than insertions or deletions.

#### **3.2 Red-Black Trees**

**Overview:**
A **Red-Black Tree** is another type of self-balancing binary search tree. It ensures that the tree remains approximately balanced, providing O(log n) time complexity for insertions, deletions, and searches. Red-Black Trees are widely used in many libraries and systems due to their balance between performance and complexity.

**Topics Covered:**
- **Red-Black Tree Properties**
- **Node Coloring**
- **Rotations and Recoloring**
- **Insertion and Deletion Algorithms**

**Detailed Explanation:**

**Red-Black Tree Properties:**
1. **Each node is either red or black.**
2. **The root is always black.**
3. **All leaves (NIL nodes) are black.**
4. **Red nodes cannot have red children (no two reds in a row).**
5. **Every path from a node to its descendant NIL nodes contains the same number of black nodes (black-height).**

**Rotations and Recoloring:**
Similar to AVL trees, Red-Black Trees use rotations and recoloring to maintain balance after insertions and deletions.

**Implementation in Java:**

Implementing a full Red-Black Tree from scratch is quite involved. Instead, we'll provide a simplified version focusing on insertion with balancing.

```java
class RedBlackTree {
    private final int RED = 0;
    private final int BLACK = 1;

    class Node {
        int data;
        int color;
        Node left, right, parent;

        Node(int data) {
            this.data = data;
            this.color = RED;
            this.left = null;
            this.right = null;
            this.parent = null;
        }
    }

    private Node root;

    // Left rotate
    private void leftRotate(Node x) {
        Node y = x.right;
        x.right = y.left;
        if (y.left != null)
            y.left.parent = x;
        y.parent = x.parent;
        if (x.parent == null)
            root = y;
        else if (x == x.parent.left)
            x.parent.left = y;
        else
            x.parent.right = y;
        y.left = x;
        x.parent = y;
    }

    // Right rotate
    private void rightRotate(Node y) {
        Node x = y.left;
        y.left = x.right;
        if (x.right != null)
            x.right.parent = y;
        x.parent = y.parent;
        if (y.parent == null)
            root = x;
        else if (y == y.parent.left)
            y.parent.left = x;
        else
            y.parent.right = x;
        x.right = y;
        y.parent = x;
    }

    // Insert a node
    public void insert(int data) {
        Node node = new Node(data);
        Node y = null;
        Node x = root;

        while (x != null) {
            y = x;
            if (node.data < x.data)
                x = x.left;
            else
                x = x.right;
        }

        node.parent = y;
        if (y == null)
            root = node;
        else if (node.data < y.data)
            y.left = node;
        else
            y.right = node;

        // Fix Red-Black Tree properties
        fixInsert(node);
    }

    private void fixInsert(Node k) {
        while (k != root && k.parent.color == RED) {
            if (k.parent == k.parent.parent.left) {
                Node uncle = k.parent.parent.right;
                if (uncle != null && uncle.color == RED) {
                    // Case 1: Uncle is red
                    k.parent.color = BLACK;
                    uncle.color = BLACK;
                    k.parent.parent.color = RED;
                    k = k.parent.parent;
                } else {
                    if (k == k.parent.right) {
                        // Case 2: Uncle is black and node is right child
                        k = k.parent;
                        leftRotate(k);
                    }
                    // Case 3: Uncle is black and node is left child
                    k.parent.color = BLACK;
                    k.parent.parent.color = RED;
                    rightRotate(k.parent.parent);
                }
            } else {
                Node uncle = k.parent.parent.left;
                if (uncle != null && uncle.color == RED) {
                    // Mirror Case 1
                    k.parent.color = BLACK;
                    uncle.color = BLACK;
                    k.parent.parent.color = RED;
                    k = k.parent.parent;
                } else {
                    if (k == k.parent.left) {
                        // Mirror Case 2
                        k = k.parent;
                        rightRotate(k);
                    }
                    // Mirror Case 3
                    k.parent.color = BLACK;
                    k.parent.parent.color = RED;
                    leftRotate(k.parent.parent);
                }
            }
        }
        root.color = BLACK;
    }

    // In-order traversal
    public void inorder() {
        inorderRec(root);
        System.out.println();
    }

    private void inorderRec(Node node) {
        if (node != null) {
            inorderRec(node.left);
            System.out.print(node.data + " ");
            inorderRec(node.right);
        }
    }

    // Example usage
    public static void main(String[] args) {
        RedBlackTree tree = new RedBlackTree();
        tree.insert(10);
        tree.insert(20);
        tree.insert(30);
        tree.insert(15);
        tree.insert(25);
        tree.insert(5);
        tree.insert(1);

        System.out.println("Inorder traversal of Red-Black Tree:");
        tree.inorder();
        // Output: 1 5 10 15 20 25 30 
    }
}
```

**Explanation:**
- **Node Class:** Each node has a color (RED or BLACK), data, and references to its left, right, and parent nodes.
- **Rotations:** Similar to AVL trees, left and right rotations are used to rebalance the tree.
- **Insertion (`insert`):** Inserts a node following BST rules and then calls `fixInsert` to maintain Red-Black properties.
- **Fix Insert (`fixInsert`):** Handles different cases based on the color of the node's uncle to restore balance and coloring rules.

**Advantages of Red-Black Trees:**
- **Efficient Balancing:** Less strict balancing compared to AVL trees, allowing for faster insertions and deletions.
- **Widely Used:** Employed in many standard libraries (e.g., Java's `TreeMap` and `TreeSet`).

#### **3.3 Comparison: AVL Trees vs. Red-Black Trees**

**Overview:**
While both AVL and Red-Black Trees are self-balancing BSTs, they differ in their balancing strategies and use-cases.

**Key Differences:**
- **Balancing Strictness:**
  - **AVL Trees:** More rigidly balanced, resulting in better search performance.
  - **Red-Black Trees:** Less strictly balanced, offering faster insertion and deletion.
- **Use-Cases:**
  - **AVL Trees:** Suitable for applications where search operations are more frequent.
  - **Red-Black Trees:** Ideal for scenarios with frequent insertions and deletions.

**Visual Representation:**

| Feature             | AVL Trees                        | Red-Black Trees                 |
|---------------------|----------------------------------|---------------------------------|
| Balancing           | Height-balanced (balance factor ≤1) | Color-balanced (5 properties)    |
| Rotations           | Potentially more rotations      | Fewer rotations on average      |
| Search Efficiency   | Slightly faster searches        | Slightly slower searches        |
| Insertion/Deletion  | Slower due to strict balancing  | Faster due to relaxed balancing |
| Use in Libraries    | Less common in standard libraries | Common in standard libraries (e.g., Java) |

---

### **4. Tries (Prefix Trees)**

#### **4.1 Implementation and Applications in String Searching**

**Overview:**
A **Trie**, also known as a **Prefix Tree**, is a tree-like data structure used to efficiently store and retrieve keys in a dataset of strings. Tries are particularly effective for tasks involving prefix searches, autocomplete systems, and spell checking.

**Topics Covered:**
- **Trie Structure and Properties**
- **Insertion and Search Operations**
- **Applications of Tries**
- **Space Optimization Techniques**

**Detailed Explanation:**

**Trie Structure:**
- **Nodes:** Each node represents a character of a string.
- **Root Node:** Represents an empty string.
- **Children:** Each node can have multiple children, each corresponding to a different character.
- **End of Word Marker:** Indicates that a complete word ends at that node.

**Implementation in Java:**

```java
import java.util.HashMap;
import java.util.Map;

class Trie {
    class TrieNode {
        Map<Character, TrieNode> children = new HashMap<>();
        boolean isEndOfWord;

        TrieNode() {
            isEndOfWord = false;
        }
    }

    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    // Insert a word into the trie
    public void insert(String word) {
        TrieNode node = root;
        for(char ch : word.toCharArray()) {
            node = node.children.computeIfAbsent(ch, c -> new TrieNode());
        }
        node.isEndOfWord = true;
    }

    // Search for a word in the trie
    public boolean search(String word) {
        TrieNode node = root;
        for(char ch : word.toCharArray()) {
            node = node.children.get(ch);
            if(node == null)
                return false;
        }
        return node.isEndOfWord;
    }

    // Check if any word in the trie starts with the given prefix
    public boolean startsWith(String prefix) {
        TrieNode node = root;
        for(char ch : prefix.toCharArray()) {
            node = node.children.get(ch);
            if(node == null)
                return false;
        }
        return true;
    }

    // Example usage
    public static void main(String[] args) {
        Trie trie = new Trie();
        trie.insert("apple");
        trie.insert("app");
        trie.insert("application");

        System.out.println(trie.search("app"));       // true
        System.out.println(trie.search("appl"));      // false
        System.out.println(trie.startsWith("appl"));  // true
        System.out.println(trie.search("apple"));     // true
        System.out.println(trie.search("application"));// true
        System.out.println(trie.startsWith("banana")); // false
    }
}
```

**Explanation:**
- **TrieNode Class:** Each node contains a map of children (keyed by character) and a boolean flag indicating if it marks the end of a word.
- **Insertion (`insert`):** Iteratively adds characters of the word, creating new nodes as necessary. Marks the end of the word.
- **Search (`search`):** Traverses the trie based on the characters of the word. Returns true only if the entire word exists and is marked as an end.
- **Prefix Search (`startsWith`):** Similar to search but returns true as long as the prefix exists, regardless of whether it's marked as an end of a word.

**Applications of Tries:**
- **Autocomplete Systems:** Suggesting words based on user input prefixes.
- **Spell Checking:** Detecting valid words and suggesting corrections.
- **IP Routing:** Efficiently managing routing tables.
- **Pattern Matching:** Searching for patterns within large datasets.

**Space Optimization Techniques:**
- **Compressed Tries (Radix Trees):** Merges nodes with single children to reduce space.
- **Bitwise Tries:** Uses bit manipulation for specific applications like IP routing.

---

### **5. Union-Find Structures**

#### **5.1 Disjoint Set Implementation**

**Overview:**
The **Union-Find** or **Disjoint Set** data structure keeps track of a set of elements partitioned into disjoint (non-overlapping) subsets. It provides efficient operations to merge sets and determine whether elements are in the same set. This structure is essential for algorithms like Kruskal’s Minimum Spanning Tree and detecting cycles in graphs.

**Topics Covered:**
- **Disjoint Set Forests**
- **Union by Rank**
- **Path Compression**
- **Applications of Union-Find**

**Detailed Explanation:**

**Disjoint Set Forest:**
A collection of trees where each tree represents a set. Each node points to its parent, and the root of the tree represents the set identifier.

**Key Operations:**
- **Find:** Determines the root of the set containing a particular element.
- **Union:** Merges two sets into a single set.

**Optimizations:**
- **Union by Rank:** Always attach the smaller tree to the root of the larger tree to keep trees shallow.
- **Path Compression:** Flattens the structure of the tree whenever `find` is called, by making each node on the path point directly to the root.

**Implementation in Java:**

```java
class UnionFind {
    private int[] parent;
    private int[] rank;

    // Initialize Union-Find structure
    public UnionFind(int size) {
        parent = new int[size];
        rank = new int[size];
        for(int i=0; i<size; i++) {
            parent[i] = i; // Each element is its own parent initially
            rank[i] = 0;   // Rank is initially zero
        }
    }

    // Find the root of the set containing x with path compression
    public int find(int x) {
        if(parent[x] != x)
            parent[x] = find(parent[x]); // Path compression
        return parent[x];
    }

    // Union the sets containing x and y using union by rank
    public void union(int x, int y) {
        int xRoot = find(x);
        int yRoot = find(y);

        if(xRoot == yRoot)
            return; // Already in the same set

        // Union by rank
        if(rank[xRoot] < rank[yRoot]) {
            parent[xRoot] = yRoot;
        }
        else if(rank[xRoot] > rank[yRoot]) {
            parent[yRoot] = xRoot;
        }
        else {
            parent[yRoot] = xRoot;
            rank[xRoot]++;
        }
    }

    // Check if two elements are in the same set
    public boolean isConnected(int x, int y) {
        return find(x) == find(y);
    }

    // Example usage
    public static void main(String[] args) {
        UnionFind uf = new UnionFind(5); // Elements 0 to 4

        uf.union(0, 1);
        uf.union(1, 2);
        uf.union(3, 4);

        System.out.println(uf.isConnected(0, 2)); // true
        System.out.println(uf.isConnected(0, 4)); // false

        uf.union(2, 4);

        System.out.println(uf.isConnected(0, 4)); // true
    }
}
```

**Explanation:**
- **Initialization:** Each element starts as its own parent with rank 0.
- **Find (`find`):** Recursively finds the root of the set, applying path compression by making each node on the path point directly to the root.
- **Union (`union`):** Merges two sets by attaching the root of one set to the root of the other, using rank to determine which root becomes the new parent.
- **isConnected:** Checks if two elements share the same root, indicating they belong to the same set.

**Advantages:**
- **Efficiency:** Nearly constant time operations due to path compression and union by rank.
- **Simplicity:** Easy to implement and understand.

**Applications of Union-Find:**
- **Kruskal’s Minimum Spanning Tree Algorithm:** Efficiently determines whether adding an edge creates a cycle.
- **Network Connectivity:** Determines if two nodes are connected.
- **Image Processing:** Identifies connected components in binary images.
- **Percolation Theory:** Models fluid flow through porous materials.

---

## **Summary and Exercises**

### **Summary:**
This module has introduced advanced data structures that are integral for solving complex algorithmic problems efficiently:

- **Heaps and Priority Queues:** Learned about min-heaps and max-heaps, their implementations, and the Heap Sort algorithm.
- **Graphs:** Explored different graph representations (adjacency matrix and list), and the distinction between weighted and unweighted graphs.
- **Balanced Search Trees:** Delved into AVL Trees and Red-Black Trees, understanding their balancing mechanisms and use-cases.
- **Tries:** Understood the structure and applications of prefix trees in string searching and related tasks.
- **Union-Find Structures:** Implemented disjoint set operations with optimizations like path compression and union by rank, and explored their applications.

### **Exercises:**

1. **Heaps and Priority Queues:**
   - **MinHeap Implementation:**
     - Extend the `MinHeap` class to include a `decreaseKey` method that decreases the value of a specific element and maintains the heap property.
   - **Heap Sort Challenge:**
     - Modify the `HeapSort` implementation to sort an array of objects based on a specific attribute (e.g., sorting an array of `Employee` objects by salary).

2. **Graphs:**
   - **Graph Traversal:**
     - Implement Depth-First Search (DFS) and Breadth-First Search (BFS) for both adjacency matrix and adjacency list representations.
   - **Cycle Detection:**
     - Write a Java program to detect cycles in an undirected graph using the Union-Find structure.
   - **Dijkstra’s Algorithm:**
     - Implement Dijkstra’s algorithm to find the shortest path from a source node to all other nodes in a weighted graph.

3. **Balanced Search Trees:**
   - **AVL Tree Deletion:**
     - Extend the `AVLTree` class to include a `delete` method that removes a node and maintains the AVL balancing.
   - **Red-Black Tree Deletion:**
     - Implement the deletion operation for the `RedBlackTree` class, ensuring all Red-Black properties are preserved.

4. **Tries:**
   - **Autocomplete System:**
     - Using the `Trie` implementation, create an autocomplete feature that suggests possible word completions based on a given prefix.
   - **Pattern Matching:**
     - Implement a function to find all words in the trie that match a given pattern with wildcards (e.g., `a*le` matches `apple`, `ample`).

5. **Union-Find Structures:**
   - **Connected Components:**
     - Given a graph, use the Union-Find structure to determine the number of connected components.
   - **Kruskal’s MST:**
     - Implement Kruskal’s algorithm using the Union-Find structure to find the Minimum Spanning Tree of a connected, weighted graph.

### **Further Reading and Resources:**

- **Books:**
  - *Introduction to Algorithms* by Cormen, Leiserson, Rivest, and Stein.
  - *Algorithms* by Robert Sedgewick and Kevin Wayne.
  - *Data Structures and Algorithm Analysis in Java* by Mark Allen Weiss.

- **Online Tutorials:**
  - [GeeksforGeeks Data Structures](https://www.geeksforgeeks.org/data-structures/)
  - [LeetCode](https://leetcode.com/) for practicing data structure problems.
  - [HackerRank](https://www.hackerrank.com/domains/data-structures) for data structures challenges.

- **Video Lectures:**
  - [MIT OpenCourseWare - Advanced Data Structures](https://ocw.mit.edu/courses/6-851-advanced-data-structures-fall-2012/)
  - [Stanford University - CS 166: Data Structures](https://www.youtube.com/playlist?list=PLoROMvodv4rOFZnDyrlW3-nI7tMLtmiJZ)
  - [Harvard's CS50 on YouTube](https://www.youtube.com/user/cs50tv)

- **Interactive Platforms:**
  - [VisuAlgo](https://visualgo.net/en) for visualizing data structures and algorithms.
  - [Algorithm Visualizer](https://algorithm-visualizer.org/) for step-by-step algorithm execution.

---

By mastering these advanced data structures, you will significantly enhance your problem-solving toolkit, enabling you to tackle a wide array of complex algorithmic challenges and excel in technical interviews at leading technology companies.
