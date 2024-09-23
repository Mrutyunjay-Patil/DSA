---
tags: [DSA Java]
title: Course Module 3. Fundamental Data Structures
created: '2024-09-17T13:45:54.598Z'
modified: '2024-09-17T14:32:17.536Z'
---

# **Course Module 3. Fundamental Data Structures**

**Duration:** 2 Weeks

Mastering fundamental data structures is crucial for solving complex algorithmic problems efficiently. This module will introduce you to essential data structures, their implementations in Java, and practical applications. Whether you're transitioning from a non-IT background or enhancing your programming skills, this section will provide you with the necessary tools to excel in technical interviews at top companies like Microsoft and Google.

---

## **Week 1: Core Data Structures**

### **1. Arrays and Strings**

#### **1.1 One-dimensional and Multi-dimensional Arrays**

**Overview:**
Arrays are the simplest and most widely used data structures. They store elements of the same type in contiguous memory locations, allowing efficient access and manipulation.

**Topics Covered:**
- **One-dimensional Arrays:**
  - Declaration and Initialization
  - Accessing Elements
  - Common Operations (Traversal, Insertion, Deletion)

- **Multi-dimensional Arrays:**
  - Declaration and Initialization
  - Accessing Elements in 2D and 3D Arrays
  - Applications (Matrices, Grids)

**Detailed Explanation:**

**One-dimensional Arrays:**
An array in Java can be declared and initialized as follows:

```java
// Declaration
int[] numbers;

// Initialization
numbers = new int[5]; // Creates an array of size 5

// Declaration and Initialization
int[] primes = {2, 3, 5, 7, 11};
```

**Accessing Elements:**
Elements are accessed using their index (0-based).

```java
int firstPrime = primes[0]; // 2
int thirdPrime = primes[2]; // 5
```

**Common Operations:**

- **Traversal:**
  ```java
  for (int i = 0; i < primes.length; i++) {
      System.out.println(primes[i]);
  }

  // Enhanced for-loop
  for (int prime : primes) {
      System.out.println(prime);
  }
  ```

- **Insertion and Deletion:**
  Arrays have a fixed size. To insert or delete elements, you typically create a new array or use dynamic data structures like ArrayList.

**Multi-dimensional Arrays:**
Used to represent complex structures like matrices.

```java
// Declaration and Initialization of a 2D array
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Accessing Elements
int middle = matrix[1][1]; // 5

// Traversal
for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[i].length; j++) {
        System.out.print(matrix[i][j] + " ");
    }
    System.out.println();
}
```

**Applications:**
- **Matrices:** Used in mathematical computations.
- **Grids:** Representing game boards, maps, etc.

**Examples:**

1. **Finding the Maximum Element in an Array:**

```java
public static int findMax(int[] arr) {
    int max = arr[0];
    for (int num : arr) {
        if (num > max) {
            max = num;
        }
    }
    return max;
}
```

2. **Matrix Multiplication:**

```java
public static int[][] multiplyMatrices(int[][] a, int[][] b) {
    int rowsA = a.length;
    int colsA = a[0].length;
    int colsB = b[0].length;
    int[][] result = new int[rowsA][colsB];
    
    for(int i = 0; i < rowsA; i++) {
        for(int j = 0; j < colsB; j++) {
            for(int k = 0; k < colsA; k++) {
                result[i][j] += a[i][k] * b[k][j];
            }
        }
    }
    return result;
}
```

#### **1.2 String Manipulation Techniques**

**Overview:**
Strings are sequences of characters and are fundamental in programming. Understanding how to manipulate strings efficiently is essential for solving many problems.

**Topics Covered:**
- **String Basics:**
  - Declaration and Initialization
  - Immutable Nature of Strings

- **Common String Operations:**
  - Concatenation
  - Substrings
  - Searching and Replacing

- **StringBuilder and StringBuffer:**
  - Mutable Alternatives to String
  - Efficient String Manipulation

**Detailed Explanation:**

**String Basics:**
In Java, strings are objects of the `String` class.

```java
String greeting = "Hello, World!";
```

**Immutable Nature:**
Strings cannot be changed once created. Any modification results in a new string.

```java
String s = "Hello";
s = s + " World"; // Creates a new string "Hello World"
```

**Common String Operations:**

- **Concatenation:**
  ```java
  String firstName = "John";
  String lastName = "Doe";
  String fullName = firstName + " " + lastName; // "John Doe"
  ```

- **Substrings:**
  ```java
  String s = "Hello, World!";
  String sub = s.substring(7, 12); // "World"
  ```

- **Searching:**
  ```java
  String s = "Hello, World!";
  int index = s.indexOf("World"); // 7
  boolean contains = s.contains("Hello"); // true
  ```

- **Replacing:**
  ```java
  String s = "Hello, World!";
  String newStr = s.replace("World", "Java"); // "Hello, Java!"
  ```

**StringBuilder and StringBuffer:**
Used for mutable string manipulation, which is more efficient for multiple modifications.

```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World"); // "Hello World"
sb.insert(5, ",");
String result = sb.toString(); // "Hello, World"
```

**Examples:**

1. **Reverse a String:**

```java
public static String reverseString(String s) {
    StringBuilder sb = new StringBuilder(s);
    return sb.reverse().toString();
}
```

2. **Check if Two Strings are Anagrams:**

```java
public static boolean areAnagrams(String s1, String s2) {
    char[] a1 = s1.replaceAll("\\s", "").toLowerCase().toCharArray();
    char[] a2 = s2.replaceAll("\\s", "").toLowerCase().toCharArray();
    Arrays.sort(a1);
    Arrays.sort(a2);
    return Arrays.equals(a1, a2);
}
```

---

### **2. Linked Lists**

#### **2.1 Singly and Doubly Linked Lists**

**Overview:**
Linked Lists are dynamic data structures composed of nodes, where each node contains data and a reference to the next (and possibly previous) node. They allow efficient insertion and deletion of elements.

**Topics Covered:**
- **Singly Linked Lists:**
  - Structure and Components
  - Basic Operations

- **Doubly Linked Lists:**
  - Structure with Previous and Next Pointers
  - Enhanced Operations

**Detailed Explanation:**

**Singly Linked Lists:**
Each node points to the next node.

```java
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class SinglyLinkedList {
    Node head;

    // Insert at the beginning
    public void insertAtHead(int data) {
        Node newNode = new Node(data);
        newNode.next = head;
        head = newNode;
    }

    // Insert at the end
    public void insertAtEnd(int data) {
        if (head == null) {
            head = new Node(data);
            return;
        }
        Node current = head;
        while (current.next != null) {
            current = current.next;
        }
        current.next = new Node(data);
    }

    // Display the list
    public void display() {
        Node current = head;
        while (current != null) {
            System.out.print(current.data + " -> ");
            current = current.next;
        }
        System.out.println("null");
    }
}
```

**Doubly Linked Lists:**
Each node points to both the next and previous nodes, allowing bidirectional traversal.

```java
class DoublyNode {
    int data;
    DoublyNode next;
    DoublyNode prev;

    DoublyNode(int data) {
        this.data = data;
        this.next = null;
        this.prev = null;
    }
}

class DoublyLinkedList {
    DoublyNode head;

    // Insert at the beginning
    public void insertAtHead(int data) {
        DoublyNode newNode = new DoublyNode(data);
        newNode.next = head;
        if (head != null) {
            head.prev = newNode;
        }
        head = newNode;
    }

    // Insert at the end
    public void insertAtEnd(int data) {
        if (head == null) {
            head = new DoublyNode(data);
            return;
        }
        DoublyNode current = head;
        while (current.next != null) {
            current = current.next;
        }
        DoublyNode newNode = new DoublyNode(data);
        current.next = newNode;
        newNode.prev = current;
    }

    // Display the list forward
    public void displayForward() {
        DoublyNode current = head;
        while (current != null) {
            System.out.print(current.data + " <-> ");
            current = current.next;
        }
        System.out.println("null");
    }

    // Display the list backward
    public void displayBackward() {
        DoublyNode current = head;
        if (current == null) return;
        while (current.next != null) {
            current = current.next;
        }
        while (current != null) {
            System.out.print(current.data + " <-> ");
            current = current.prev;
        }
        System.out.println("null");
    }
}
```

**Advantages:**
- **Singly Linked Lists:** Simpler and require less memory.
- **Doubly Linked Lists:** Allow efficient reverse traversal and easier deletion of nodes.

**Applications:**
- Implementing stacks and queues.
- Browser history navigation.
- Music playlist management.

#### **2.2 Common Operations (Insertion, Deletion, Reversal)**

**Overview:**
Efficiently performing operations on linked lists is essential for optimizing performance in various applications.

**Topics Covered:**
- **Insertion:**
  - At the Head
  - At the Tail
  - At a Specific Position

- **Deletion:**
  - From the Head
  - From the Tail
  - By Value or Position

- **Reversal:**
  - Iterative Method
  - Recursive Method

**Detailed Explanation:**

**Insertion:**

- **At the Head:**
  ```java
  public void insertAtHead(int data) {
      Node newNode = new Node(data);
      newNode.next = head;
      head = newNode;
  }
  ```

- **At the Tail:**
  ```java
  public void insertAtEnd(int data) {
      Node newNode = new Node(data);
      if (head == null) {
          head = newNode;
          return;
      }
      Node current = head;
      while (current.next != null) {
          current = current.next;
      }
      current.next = newNode;
  }
  ```

- **At a Specific Position:**
  ```java
  public void insertAtPosition(int data, int position) {
      if (position == 0) {
          insertAtHead(data);
          return;
      }
      Node newNode = new Node(data);
      Node current = head;
      for (int i = 0; i < position - 1 && current != null; i++) {
          current = current.next;
      }
      if (current == null) {
          System.out.println("Position out of bounds");
          return;
      }
      newNode.next = current.next;
      current.next = newNode;
  }
  ```

**Deletion:**

- **From the Head:**
  ```java
  public void deleteFromHead() {
      if (head == null) return;
      head = head.next;
  }
  ```

- **From the Tail:**
  ```java
  public void deleteFromEnd() {
      if (head == null) return;
      if (head.next == null) {
          head = null;
          return;
      }
      Node current = head;
      while (current.next.next != null) {
          current = current.next;
      }
      current.next = null;
  }
  ```

- **By Value:**
  ```java
  public void deleteByValue(int value) {
      if (head == null) return;
      if (head.data == value) {
          head = head.next;
          return;
      }
      Node current = head;
      while (current.next != null && current.next.data != value) {
          current = current.next;
      }
      if (current.next == null) {
          System.out.println("Value not found");
          return;
      }
      current.next = current.next.next;
  }
  ```

**Reversal:**

- **Iterative Method:**
  ```java
  public void reverseIterative() {
      Node prev = null;
      Node current = head;
      Node next = null;
      while (current != null) {
          next = current.next;
          current.next = prev;
          prev = current;
          current = next;
      }
      head = prev;
  }
  ```

- **Recursive Method:**
  ```java
  public Node reverseRecursive(Node current, Node prev) {
      if (current == null) return prev;
      Node next = current.next;
      current.next = prev;
      return reverseRecursive(next, current);
  }

  // To call the recursive reverse
  public void reverseRecursive() {
      head = reverseRecursive(head, null);
  }
  ```

**Examples:**

1. **Detecting a Cycle in a Linked List:**

```java
public boolean hasCycle() {
    if (head == null) return false;
    Node slow = head;
    Node fast = head.next;
    while (fast != null && fast.next != null) {
        if (slow == fast) return true;
        slow = slow.next;
        fast = fast.next.next;
    }
    return false;
}
```

2. **Finding the Middle Element:**

```java
public int findMiddle() {
    if (head == null) throw new NoSuchElementException("List is empty");
    Node slow = head;
    Node fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow.data;
}
```

---

## **Week 2: Advanced Data Structures**

### **3. Stacks and Queues**

#### **3.1 Implementation using Arrays and Linked Lists**

**Overview:**
Stacks and queues are abstract data types that follow specific orderings for element insertion and removal. They are fundamental for various algorithmic solutions and system processes.

**Topics Covered:**
- **Stacks:**
  - LIFO (Last-In-First-Out) Principle
  - Implementation using Arrays
  - Implementation using Linked Lists

- **Queues:**
  - FIFO (First-In-First-Out) Principle
  - Implementation using Arrays
  - Implementation using Linked Lists

**Detailed Explanation:**

**Stacks:**

- **LIFO Principle:**
  The last element added is the first to be removed.

- **Implementation using Arrays:**
  ```java
  class StackArray {
      private int[] stack;
      private int top;
      private int capacity;

      StackArray(int size) {
          stack = new int[size];
          capacity = size;
          top = -1;
      }

      public void push(int x) {
          if (top == capacity - 1) {
              System.out.println("Stack Overflow");
              return;
          }
          stack[++top] = x;
      }

      public int pop() {
          if (top == -1) {
              System.out.println("Stack Underflow");
              return -1;
          }
          return stack[top--];
      }

      public int peek() {
          if (top == -1) {
              System.out.println("Stack is empty");
              return -1;
          }
          return stack[top];
      }

      public boolean isEmpty() {
          return top == -1;
      }
  }
  ```

- **Implementation using Linked Lists:**
  ```java
  class StackNode {
      int data;
      StackNode next;

      StackNode(int data) {
          this.data = data;
          this.next = null;
      }
  }

  class StackLinkedList {
      private StackNode top;

      public StackLinkedList() {
          top = null;
      }

      public void push(int data) {
          StackNode newNode = new StackNode(data);
          newNode.next = top;
          top = newNode;
      }

      public int pop() {
          if (top == null) {
              System.out.println("Stack Underflow");
              return -1;
          }
          int value = top.data;
          top = top.next;
          return value;
      }

      public int peek() {
          if (top == null) {
              System.out.println("Stack is empty");
              return -1;
          }
          return top.data;
      }

      public boolean isEmpty() {
          return top == null;
      }
  }
  ```

**Queues:**

- **FIFO Principle:**
  The first element added is the first to be removed.

- **Implementation using Arrays:**
  ```java
  class QueueArray {
      private int[] queue;
      private int front, rear, size, capacity;

      QueueArray(int capacity) {
          this.capacity = capacity;
          queue = new int[capacity];
          front = 0;
          rear = -1;
          size = 0;
      }

      public void enqueue(int x) {
          if (size == capacity) {
              System.out.println("Queue Overflow");
              return;
          }
          rear = (rear + 1) % capacity;
          queue[rear] = x;
          size++;
      }

      public int dequeue() {
          if (size == 0) {
              System.out.println("Queue Underflow");
              return -1;
          }
          int value = queue[front];
          front = (front + 1) % capacity;
          size--;
          return value;
      }

      public boolean isEmpty() {
          return size == 0;
      }
  }
  ```

- **Implementation using Linked Lists:**
  ```java
  class QueueNode {
      int data;
      QueueNode next;

      QueueNode(int data) {
          this.data = data;
          this.next = null;
      }
  }

  class QueueLinkedList {
      private QueueNode front, rear;

      public QueueLinkedList() {
          front = rear = null;
      }

      public void enqueue(int data) {
          QueueNode newNode = new QueueNode(data);
          if (rear == null) {
              front = rear = newNode;
              return;
          }
          rear.next = newNode;
          rear = newNode;
      }

      public int dequeue() {
          if (front == null) {
              System.out.println("Queue Underflow");
              return -1;
          }
          int value = front.data;
          front = front.next;
          if (front == null) rear = null;
          return value;
      }

      public boolean isEmpty() {
          return front == null;
      }
  }
  ```

**Advantages and Use-Cases:**

- **Stacks:**
  - Function call management (call stack)
  - Expression evaluation (infix to postfix)
  - Undo mechanisms in applications

- **Queues:**
  - Order processing
  - BFS (Breadth-First Search) in graphs
  - Printer job management

#### **3.2 Applications and Problem Solving**

**Overview:**
Understanding the practical applications of stacks and queues enhances problem-solving skills, enabling you to tackle complex algorithmic challenges effectively.

**Topics Covered:**
- **Stacks:**
  - Balanced Parentheses
  - Infix to Postfix Conversion
  - Evaluating Postfix Expressions

- **Queues:**
  - Level Order Traversal in Trees
  - Implementing BFS
  - Circular Queues and Priority Queues

**Detailed Explanation:**

**Stacks Applications:**

1. **Balanced Parentheses:**
   - **Problem:** Check if an expression has balanced parentheses.
   - **Solution:**
     Use a stack to track opening brackets and ensure they are properly closed.

   ```java
   public boolean isBalanced(String expr) {
       Stack<Character> stack = new Stack<>();
       for (char ch : expr.toCharArray()) {
           if (ch == '(' || ch == '{' || ch == '[') {
               stack.push(ch);
           } else if (ch == ')' || ch == '}' || ch == ']') {
               if (stack.isEmpty()) return false;
               char open = stack.pop();
               if (!isMatchingPair(open, ch)) return false;
           }
       }
       return stack.isEmpty();
   }

   private boolean isMatchingPair(char open, char close) {
       return (open == '(' && close == ')') ||
              (open == '{' && close == '}') ||
              (open == '[' && close == ']');
   }
   ```

2. **Infix to Postfix Conversion:**
   - **Problem:** Convert an infix expression (e.g., `A + B * C`) to postfix (e.g., `A B C * +`).
   - **Solution:**
     Use a stack to handle operator precedence and associativity.

   ```java
   public String infixToPostfix(String expr) {
       StringBuilder result = new StringBuilder();
       Stack<Character> stack = new Stack<>();
       for (char ch : expr.toCharArray()) {
           if (Character.isLetterOrDigit(ch)) {
               result.append(ch);
           } else if (ch == '(') {
               stack.push(ch);
           } else if (ch == ')') {
               while (!stack.isEmpty() && stack.peek() != '(') {
                   result.append(stack.pop());
               }
               stack.pop(); // Remove '('
           } else { // Operator
               while (!stack.isEmpty() && precedence(ch) <= precedence(stack.peek())) {
                   result.append(stack.pop());
               }
               stack.push(ch);
           }
       }
       while (!stack.isEmpty()) {
           result.append(stack.pop());
       }
       return result.toString();
   }

   private int precedence(char op) {
       switch (op) {
           case '+':
           case '-':
               return 1;
           case '*':
           case '/':
               return 2;
           case '^':
               return 3;
       }
       return -1;
   }
   ```

**Queues Applications:**

1. **Level Order Traversal in Trees:**
   - **Problem:** Traverse a binary tree level by level.
   - **Solution:**
     Use a queue to keep track of nodes at each level.

   ```java
   public void levelOrderTraversal(TreeNode root) {
       if (root == null) return;
       Queue<TreeNode> queue = new LinkedList<>();
       queue.add(root);
       while (!queue.isEmpty()) {
           TreeNode current = queue.poll();
           System.out.print(current.val + " ");
           if (current.left != null) queue.add(current.left);
           if (current.right != null) queue.add(current.right);
       }
   }
   ```

2. **Implementing BFS (Breadth-First Search):**
   - **Problem:** Traverse or search tree or graph data structures.
   - **Solution:**
     BFS uses a queue to explore nodes level by level.

   ```java
   public void bfs(int start, List<List<Integer>> adjList) {
       boolean[] visited = new boolean[adjList.size()];
       Queue<Integer> queue = new LinkedList<>();
       visited[start] = true;
       queue.add(start);
       while (!queue.isEmpty()) {
           int node = queue.poll();
           System.out.print(node + " ");
           for (int neighbor : adjList.get(node)) {
               if (!visited[neighbor]) {
                   visited[neighbor] = true;
                   queue.add(neighbor);
               }
           }
       }
   }
   ```

**Examples:**

1. **Implementing a Min Stack (Stack with getMin in O(1)):**

```java
class MinStack {
    private Stack<Integer> stack;
    private Stack<Integer> minStack;

    public MinStack() {
        stack = new Stack<>();
        minStack = new Stack<>();
    }

    public void push(int x) {
        stack.push(x);
        if (minStack.isEmpty() || x <= minStack.peek()) {
            minStack.push(x);
        }
    }

    public void pop() {
        if (stack.pop().equals(minStack.peek())) {
            minStack.pop();
        }
    }

    public int getMin() {
        return minStack.peek();
    }
}
```

2. **Circular Queue Implementation:**

```java
class CircularQueue {
    private int[] queue;
    private int front, rear, size, capacity;

    CircularQueue(int capacity) {
        this.capacity = capacity;
        queue = new int[capacity];
        front = 0;
        rear = -1;
        size = 0;
    }

    public void enqueue(int x) {
        if (size == capacity) {
            System.out.println("Queue Overflow");
            return;
        }
        rear = (rear + 1) % capacity;
        queue[rear] = x;
        size++;
    }

    public int dequeue() {
        if (size == 0) {
            System.out.println("Queue Underflow");
            return -1;
        }
        int value = queue[front];
        front = (front + 1) % capacity;
        size--;
        return value;
    }

    public boolean isEmpty() {
        return size == 0;
    }
}
```

---

### **4. Hash Tables and Hash Functions**

#### **4.1 Implementation of Hash Maps and Sets**

**Overview:**
Hash tables provide efficient insertion, deletion, and lookup operations. They are fundamental for implementing associative arrays and sets.

**Topics Covered:**
- **Hash Maps:**
  - Structure and Components
  - Implementing using Arrays (Separate Chaining)
  - Handling Collisions

- **Hash Sets:**
  - Utilizing Hash Maps for Set Operations
  - Implementing Basic Set Operations

**Detailed Explanation:**

**Hash Maps:**
A hash map stores key-value pairs and allows quick access to values based on keys.

- **Structure:**
  - **Buckets:** An array where each index corresponds to a bucket.
  - **Nodes:** Each bucket contains a linked list or another structure to handle collisions.

- **Implementation using Separate Chaining:**
  ```java
  class HashNode<K, V> {
      K key;
      V value;
      HashNode<K, V> next;

      public HashNode(K key, V value) {
          this.key = key;
          this.value = value;
          this.next = null;
      }
  }

  class HashMapCustom<K, V> {
      private int capacity;
      private HashNode<K, V>[] buckets;

      @SuppressWarnings("unchecked")
      public HashMapCustom(int capacity) {
          this.capacity = capacity;
          buckets = new HashNode[capacity];
      }

      private int getBucketIndex(K key) {
          return Math.abs(key.hashCode()) % capacity;
      }

      public void put(K key, V value) {
          int index = getBucketIndex(key);
          HashNode<K, V> head = buckets[index];
          // Check if key exists
          while (head != null) {
              if (head.key.equals(key)) {
                  head.value = value;
                  return;
              }
              head = head.next;
          }
          // Insert new node
          head = buckets[index];
          HashNode<K, V> newNode = new HashNode<>(key, value);
          newNode.next = head;
          buckets[index] = newNode;
      }

      public V get(K key) {
          int index = getBucketIndex(key);
          HashNode<K, V> head = buckets[index];
          while (head != null) {
              if (head.key.equals(key)) {
                  return head.value;
              }
              head = head.next;
          }
          return null;
      }

      public void remove(K key) {
          int index = getBucketIndex(key);
          HashNode<K, V> head = buckets[index];
          HashNode<K, V> prev = null;
          while (head != null) {
              if (head.key.equals(key)) {
                  if (prev != null) {
                      prev.next = head.next;
                  } else {
                      buckets[index] = head.next;
                  }
                  return;
              }
              prev = head;
              head = head.next;
          }
      }
  }
  ```

**Hash Sets:**
A hash set stores unique elements and is typically implemented using a hash map where keys are the set elements and values are dummy or irrelevant.

- **Implementation:**
  ```java
  class HashSetCustom<K> {
      private HashMapCustom<K, Boolean> map;

      public HashSetCustom(int capacity) {
          map = new HashMapCustom<>(capacity);
      }

      public void add(K key) {
          map.put(key, true);
      }

      public void remove(K key) {
          map.remove(key);
      }

      public boolean contains(K key) {
          return map.get(key) != null;
      }
  }
  ```

**Advantages:**
- **Fast Access:** Average time complexity of O(1) for insertion, deletion, and lookup.
- **Flexible Key Types:** Can use any object as a key, provided it correctly implements `hashCode()` and `equals()`.

**Applications:**
- Implementing caches.
- Database indexing.
- Counting frequency of elements.

#### **4.2 Collision Resolution Techniques**

**Overview:**
Collisions occur when multiple keys hash to the same bucket. Effective collision resolution ensures the hash table maintains its performance.

**Topics Covered:**
- **Separate Chaining:**
  - Using Linked Lists or Balanced Trees
  - Implementation Details

- **Open Addressing:**
  - Linear Probing
  - Quadratic Probing
  - Double Hashing

- **Rehashing:**
  - Resizing the Hash Table
  - Recomputing Hashes

**Detailed Explanation:**

**Separate Chaining:**
Each bucket contains a linked list (or another data structure) of all elements hashing to that index.

- **Advantages:**
  - Simple to implement.
  - Handles high load factors gracefully.

- **Disadvantages:**
  - Extra memory for pointers.
  - Potentially longer linked lists can degrade performance.

**Open Addressing:**
All elements are stored within the hash table array itself. Upon collision, find another slot using a probing sequence.

- **Linear Probing:**
  ```java
  public void putLinearProbing(int key, int value) {
      int index = key % capacity;
      while (table[index] != null && table[index].key != key) {
          index = (index + 1) % capacity;
      }
      table[index] = new HashNode<>(key, value);
  }
  ```

- **Quadratic Probing:**
  ```java
  public void putQuadraticProbing(int key, int value) {
      int index = key % capacity;
      int i = 1;
      while (table[index] != null && table[index].key != key) {
          index = (index + i * i) % capacity;
          i++;
      }
      table[index] = new HashNode<>(key, value);
  }
  ```

- **Double Hashing:**
  ```java
  public void putDoubleHashing(int key, int value) {
      int index = key % capacity;
      int step = 7 - (key % 7); // Second hash function
      while (table[index] != null && table[index].key != key) {
          index = (index + step) % capacity;
      }
      table[index] = new HashNode<>(key, value);
  }
  ```

**Rehashing:**
When the load factor exceeds a threshold (e.g., 0.75), resize the hash table and re-insert all existing elements.

```java
public void rehash() {
    HashNode<K, V>[] oldBuckets = buckets;
    capacity = capacity * 2;
    buckets = new HashNode[capacity];
    for (HashNode<K, V> headNode : oldBuckets) {
        while (headNode != null) {
            put(headNode.key, headNode.value);
            headNode = headNode.next;
        }
    }
}
```

**Examples:**

1. **Implementing Double Hashing:**

```java
class DoubleHashMap<K, V> {
    private int capacity;
    private HashNode<K, V>[] table;

    @SuppressWarnings("unchecked")
    public DoubleHashMap(int capacity) {
        this.capacity = capacity;
        table = new HashNode[capacity];
    }

    private int hash1(K key) {
        return Math.abs(key.hashCode()) % capacity;
    }

    private int hash2(K key) {
        return 7 - (Math.abs(key.hashCode()) % 7);
    }

    public void put(K key, V value) {
        int index = hash1(key);
        int step = hash2(key);
        while (table[index] != null && !table[index].key.equals(key)) {
            index = (index + step) % capacity;
        }
        table[index] = new HashNode<>(key, value);
    }

    public V get(K key) {
        int index = hash1(key);
        int step = hash2(key);
        while (table[index] != null) {
            if (table[index].key.equals(key)) {
                return table[index].value;
            }
            index = (index + step) % capacity;
        }
        return null;
    }

    public void remove(K key) {
        int index = hash1(key);
        int step = hash2(key);
        while (table[index] != null) {
            if (table[index].key.equals(key)) {
                table[index] = null;
                return;
            }
            index = (index + step) % capacity;
        }
    }
}
```

2. **Handling Collisions with Separate Chaining:**

```java
public void putWithSeparateChaining(K key, V value) {
    int index = getBucketIndex(key);
    HashNode<K, V> head = buckets[index];
    while (head != null) {
        if (head.key.equals(key)) {
            head.value = value;
            return;
        }
        head = head.next;
    }
    HashNode<K, V> newNode = new HashNode<>(key, value);
    newNode.next = buckets[index];
    buckets[index] = newNode;
}
```

---

### **5. Trees**

#### **5.1 Binary Trees and Binary Search Trees**

**Overview:**
Trees are hierarchical data structures consisting of nodes connected by edges. Binary trees restrict each node to have at most two children, facilitating various operations and algorithms.

**Topics Covered:**
- **Binary Trees:**
  - Structure and Properties
  - Types (Full, Complete, Perfect, Balanced)

- **Binary Search Trees (BST):**
  - BST Properties
  - Insertion, Deletion, and Search Operations
  - Balancing BSTs (Brief Overview)

**Detailed Explanation:**

**Binary Trees:**

- **Structure:**
  Each node has at most two children: left and right.

- **Types:**
  - **Full Binary Tree:** Every node has 0 or 2 children.
  - **Complete Binary Tree:** All levels are fully filled except possibly the last, which is filled from left to right.
  - **Perfect Binary Tree:** All internal nodes have two children, and all leaves are at the same level.
  - **Balanced Binary Tree:** The height difference between left and right subtrees is at most one for every node.

**Binary Search Trees (BST):**

- **Properties:**
  - Left subtree contains nodes with keys less than the parent node.
  - Right subtree contains nodes with keys greater than the parent node.
  - No duplicate nodes.

- **Implementation:**
  ```java
  class TreeNode {
      int val;
      TreeNode left, right;

      TreeNode(int val) {
          this.val = val;
          left = right = null;
      }
  }

  class BinarySearchTree {
      TreeNode root;

      public void insert(int val) {
          root = insertRec(root, val);
      }

      private TreeNode insertRec(TreeNode root, int val) {
          if (root == null) {
              root = new TreeNode(val);
              return root;
          }
          if (val < root.val)
              root.left = insertRec(root.left, val);
          else if (val > root.val)
              root.right = insertRec(root.right, val);
          return root;
      }

      public boolean search(int val) {
          return searchRec(root, val);
      }

      private boolean searchRec(TreeNode root, int val) {
          if (root == null) return false;
          if (root.val == val) return true;
          return val < root.val ? searchRec(root.left, val) : searchRec(root.right, val);
      }

      public void inorder() {
          inorderRec(root);
          System.out.println();
      }

      private void inorderRec(TreeNode root) {
          if (root != null) {
              inorderRec(root.left);
              System.out.print(root.val + " ");
              inorderRec(root.right);
          }
      }

      // Additional methods: delete, findMin, findMax, etc.
  }
  ```

**Advantages of BST:**
- **Efficient Search:** Average time complexity of O(log n) for search, insertion, and deletion.
- **Dynamic Size:** Easily accommodates dynamic data.

**Balancing BSTs:**
To maintain efficiency, BSTs can be balanced (e.g., AVL Trees, Red-Black Trees) to ensure the height remains logarithmic relative to the number of nodes.

**Applications:**
- Implementing dynamic sets and lookup tables.
- Efficient sorting algorithms.
- Priority queues.

#### **5.2 Tree Traversals (Inorder, Preorder, Postorder)**

**Overview:**
Tree traversal refers to the process of visiting each node in a tree systematically. Understanding traversal methods is essential for various tree operations and algorithms.

**Topics Covered:**
- **Inorder Traversal:**
  - Left, Root, Right
  - Application in BSTs (Sorted Order)

- **Preorder Traversal:**
  - Root, Left, Right
  - Application in Copying Trees

- **Postorder Traversal:**
  - Left, Right, Root
  - Application in Deleting Trees

**Detailed Explanation:**

**Inorder Traversal:**

- **Process:**
  1. Traverse the left subtree.
  2. Visit the root node.
  3. Traverse the right subtree.

- **Implementation:**
  ```java
  public void inorderTraversal(TreeNode root) {
      if (root != null) {
          inorderTraversal(root.left);
          System.out.print(root.val + " ");
          inorderTraversal(root.right);
      }
  }
  ```

- **Application:**
  - Produces nodes in non-decreasing order for BSTs.

**Preorder Traversal:**

- **Process:**
  1. Visit the root node.
  2. Traverse the left subtree.
  3. Traverse the right subtree.

- **Implementation:**
  ```java
  public void preorderTraversal(TreeNode root) {
      if (root != null) {
          System.out.print(root.val + " ");
          preorderTraversal(root.left);
          preorderTraversal(root.right);
      }
  }
  ```

- **Application:**
  - Used in tree copying and expression tree evaluations.

**Postorder Traversal:**

- **Process:**
  1. Traverse the left subtree.
  2. Traverse the right subtree.
  3. Visit the root node.

- **Implementation:**
  ```java
  public void postorderTraversal(TreeNode root) {
      if (root != null) {
          postorderTraversal(root.left);
          postorderTraversal(root.right);
          System.out.print(root.val + " ");
      }
  }
  ```

- **Application:**
  - Used in deleting trees and evaluating postfix expressions.

**Iterative Implementations:**
While recursive implementations are straightforward, iterative traversals using stacks or queues can be more efficient and avoid stack overflow for deep trees.

**Examples:**

1. **Iterative Inorder Traversal:**

```java
public void inorderIterative(TreeNode root) {
    Stack<TreeNode> stack = new Stack<>();
    TreeNode current = root;
    while (current != null || !stack.isEmpty()) {
        while (current != null) {
            stack.push(current);
            current = current.left;
        }
        current = stack.pop();
        System.out.print(current.val + " ");
        current = current.right;
    }
}
```

2. **Level Order Traversal (Breadth-First):**

```java
public void levelOrder(TreeNode root) {
    if (root == null) return;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.add(root);
    while (!queue.isEmpty()) {
        TreeNode current = queue.poll();
        System.out.print(current.val + " ");
        if (current.left != null) queue.add(current.left);
        if (current.right != null) queue.add(current.right);
    }
}
```

---

## **Summary and Exercises**

### **Summary:**
In this module, you have explored fundamental data structures essential for algorithmic problem-solving:

- **Arrays and Strings:** Learned about static data storage and manipulation techniques.
- **Linked Lists:** Understood dynamic data structures with efficient insertion and deletion.
- **Stacks and Queues:** Explored LIFO and FIFO principles with practical applications.
- **Hash Tables:** Gained insights into efficient key-value storage and collision resolution.
- **Trees:** Delved into hierarchical data structures with traversal methods crucial for various algorithms.

### **Exercises:**

1. **Arrays and Strings:**
   - Write a Java program to find the second largest element in an array.
   - Implement a function to check if a string is a palindrome using string manipulation techniques.

2. **Linked Lists:**
   - Create a singly linked list and implement a method to detect and remove a cycle if present.
   - Implement a doubly linked list and write a method to find the nth node from the end.

3. **Stacks and Queues:**
   - Use a stack to evaluate a postfix expression (e.g., `5 1 2 + 4 * + 3 -`).
   - Implement a queue using two stacks.

4. **Hash Tables:**
   - Design a hash map from scratch with separate chaining and implement basic operations (`put`, `get`, `remove`).
   - Use a hash set to find all unique elements in an array.

5. **Trees:**
   - Implement a binary search tree and write functions for insertion, deletion, and searching.
   - Perform inorder, preorder, and postorder traversals both recursively and iteratively.

### **Further Reading and Resources:**

- **Books:**
  - *Introduction to Algorithms* by Cormen, Leiserson, Rivest, and Stein.
  - *Data Structures and Algorithms in Java* by Robert Lafore.

- **Online Tutorials:**
  - [GeeksforGeeks Data Structures](https://www.geeksforgeeks.org/data-structures/)
  - [LeetCode](https://leetcode.com/) for practicing data structure problems.

- **Video Lectures:**
  - [MIT OpenCourseWare - Introduction to Algorithms](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-spring-2020/)
  - [Harvard's CS50 on YouTube](https://www.youtube.com/user/cs50tv)

---

By mastering these fundamental data structures, you'll build a strong foundation to tackle complex algorithmic challenges and excel in technical interviews at leading technology companies.
