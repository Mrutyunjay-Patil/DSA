---
tags: [DSA Java]
title: Course Module 8. Concurrency and Multithreading
created: '2024-09-17T14:20:20.559Z'
modified: '2024-09-17T14:32:31.451Z'
---

# **Course Module 8. Concurrency and Multithreading**

**Duration:** 1 Week

Concurrency and Multithreading are essential concepts in modern programming that allow applications to perform multiple tasks simultaneously. This module will introduce you to the fundamentals of managing threads in Java, ensuring safe access to shared resources through synchronization, and utilizing concurrent data structures for efficient multi-threaded operations. The content is designed to be simple and easy to understand, even for those new to these advanced topics.

---

## **Week 1: Understanding Concurrency and Multithreading in Java**

### **1. Thread Management in Java**

Multithreading allows a program to perform multiple tasks concurrently, improving performance and responsiveness. In Java, threads can be created and managed in various ways.

#### **1.1 Creating and Managing Threads**

**Overview:**
A thread is a lightweight subprocess that can run concurrently with other threads within a program. Java provides two primary ways to create threads:
1. **By Extending the `Thread` Class**
2. **By Implementing the `Runnable` Interface**

**Method 1: Extending the `Thread` Class**

When you extend the `Thread` class, you create a new class that inherits from `Thread` and override the `run()` method to define the task the thread will perform.

**Java Implementation:**

```java
// Extending the Thread class
class MyThread extends Thread {
    private String threadName;

    MyThread(String name) {
        this.threadName = name;
    }

    // Override the run method
    public void run() {
        System.out.println(threadName + " is running.");
        try {
            // Simulate some work with sleep
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            System.out.println(threadName + " was interrupted.");
        }
        System.out.println(threadName + " has finished.");
    }
}

// Example usage
public class ThreadExample {
    public static void main(String[] args) {
        // Create two threads
        MyThread thread1 = new MyThread("Thread 1");
        MyThread thread2 = new MyThread("Thread 2");

        // Start the threads
        thread1.start();
        thread2.start();

        // Wait for threads to finish
        try {
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            System.out.println("Main thread interrupted.");
        }

        System.out.println("All threads have finished.");
    }
}
```

**Output:**
```
Thread 1 is running.
Thread 2 is running.
Thread 1 has finished.
Thread 2 has finished.
All threads have finished.
```

**Method 2: Implementing the `Runnable` Interface**

Implementing the `Runnable` interface is more flexible, especially when your class already extends another class. You define the `run()` method within a class that implements `Runnable` and pass an instance of this class to a `Thread` object.

**Java Implementation:**

```java
// Implementing the Runnable interface
class MyRunnable implements Runnable {
    private String threadName;

    MyRunnable(String name) {
        this.threadName = name;
    }

    // Override the run method
    public void run() {
        System.out.println(threadName + " is running.");
        try {
            // Simulate some work with sleep
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            System.out.println(threadName + " was interrupted.");
        }
        System.out.println(threadName + " has finished.");
    }
}

// Example usage
public class RunnableExample {
    public static void main(String[] args) {
        // Create two runnable tasks
        MyRunnable runnable1 = new MyRunnable("Runnable 1");
        MyRunnable runnable2 = new MyRunnable("Runnable 2");

        // Create threads with runnable tasks
        Thread thread1 = new Thread(runnable1);
        Thread thread2 = new Thread(runnable2);

        // Start the threads
        thread1.start();
        thread2.start();

        // Wait for threads to finish
        try {
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            System.out.println("Main thread interrupted.");
        }

        System.out.println("All runnable threads have finished.");
    }
}
```

**Output:**
```
Runnable 1 is running.
Runnable 2 is running.
Runnable 1 has finished.
Runnable 2 has finished.
All runnable threads have finished.
```

**Key Points:**
- **`start()` Method:** Initiates the thread and calls the `run()` method in a separate call stack.
- **`run()` Method:** Contains the code that the thread will execute.
- **`join()` Method:** Allows the main thread to wait for the completion of other threads.

---

### **2. Synchronization and Locks**

When multiple threads access shared resources, it's crucial to manage access to prevent data inconsistency and ensure thread safety. Java provides synchronization mechanisms to control how threads interact with shared data.

#### **2.1 Synchronized Methods and Blocks**

**Overview:**
- **Synchronized Methods:** Methods declared with the `synchronized` keyword, ensuring that only one thread can execute them at a time for a given object.
- **Synchronized Blocks:** Blocks of code within methods that are synchronized on a specific object, offering more granular control over synchronization.

**Synchronized Methods Example:**

```java
class Counter {
    private int count = 0;

    // Synchronized method to increment the count
    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}

public class SynchronizedMethodExample {
    public static void main(String[] args) {
        Counter counter = new Counter();

        // Create a task that increments the counter 1000 times
        Runnable task = () -> {
            for (int i = 0; i < 1000; i++)
                counter.increment();
        };

        // Create two threads executing the same task
        Thread thread1 = new Thread(task);
        Thread thread2 = new Thread(task);

        // Start the threads
        thread1.start();
        thread2.start();

        // Wait for threads to finish
        try {
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            System.out.println("Threads interrupted.");
        }

        // The expected count is 2000
        System.out.println("Final count: " + counter.getCount());
    }
}
```

**Output:**
```
Final count: 2000
```

**Explanation:**
- **Synchronized `increment()` Method:** Ensures that only one thread can execute the `increment()` method at a time, preventing race conditions.
- **Result:** Both threads safely increment the counter, resulting in the correct final count.

**Synchronized Blocks Example:**

```java
class SharedResource {
    private int value = 0;

    // Method with a synchronized block
    public void add(int amount) {
        synchronized (this) {
            value += amount;
        }
    }

    public int getValue() {
        return value;
    }
}

public class SynchronizedBlockExample {
    public static void main(String[] args) {
        SharedResource resource = new SharedResource();

        // Create a task that adds to the shared resource
        Runnable task = () -> {
            for (int i = 0; i < 1000; i++)
                resource.add(1);
        };

        // Create two threads executing the same task
        Thread thread1 = new Thread(task);
        Thread thread2 = new Thread(task);

        // Start the threads
        thread1.start();
        thread2.start();

        // Wait for threads to finish
        try {
            thread1.join();
            thread2.join();
        } catch (InterruptedException e) {
            System.out.println("Threads interrupted.");
        }

        // The expected value is 2000
        System.out.println("Final value: " + resource.getValue());
    }
}
```

**Output:**
```
Final value: 2000
```

**Explanation:**
- **Synchronized Block:** Only the code within the `synchronized (this)` block is protected, allowing other parts of the method to execute concurrently if needed.
- **Result:** Similar to the synchronized method, ensuring thread-safe operations on shared data.

**Key Points:**
- **Synchronization:** Prevents multiple threads from modifying shared data simultaneously.
- **Locks:** When a method or block is synchronized, the thread acquires a lock on the specified object, ensuring exclusive access.

---

#### **2.2 Lock Objects and Conditions**

**Overview:**
While the `synchronized` keyword is straightforward, Java's `Lock` interface provides more advanced synchronization capabilities. `Lock` objects allow explicit control over locking and unlocking, and `Condition` objects enable thread coordination.

**Using `Lock` and `Condition`:**

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.locks.Condition;

class BankAccount {
    private int balance = 0;
    private Lock lock = new ReentrantLock();
    private Condition sufficientFunds = lock.newCondition();

    // Deposit method
    public void deposit(int amount) {
        lock.lock();
        try {
            balance += amount;
            System.out.println("Deposited: " + amount + ", New Balance: " + balance);
            sufficientFunds.signal(); // Notify waiting threads
        } finally {
            lock.unlock();
        }
    }

    // Withdraw method
    public void withdraw(int amount) throws InterruptedException {
        lock.lock();
        try {
            while (balance < amount) {
                System.out.println("Insufficient funds for withdrawal of " + amount + ". Waiting...");
                sufficientFunds.await(); // Wait for sufficient funds
            }
            balance -= amount;
            System.out.println("Withdrew: " + amount + ", New Balance: " + balance);
        } finally {
            lock.unlock();
        }
    }

    public int getBalance() {
        return balance;
    }
}

public class LockConditionExample {
    public static void main(String[] args) {
        BankAccount account = new BankAccount();

        // Thread to perform withdrawal
        Thread withdrawThread = new Thread(() -> {
            try {
                account.withdraw(100);
            } catch (InterruptedException e) {
                System.out.println("Withdrawal interrupted.");
            }
        });

        // Thread to perform deposit after some delay
        Thread depositThread = new Thread(() -> {
            try {
                Thread.sleep(2000); // Simulate delay
                account.deposit(150);
            } catch (InterruptedException e) {
                System.out.println("Deposit interrupted.");
            }
        });

        // Start both threads
        withdrawThread.start();
        depositThread.start();

        // Wait for threads to finish
        try {
            withdrawThread.join();
            depositThread.join();
        } catch (InterruptedException e) {
            System.out.println("Main thread interrupted.");
        }

        System.out.println("Final Balance: " + account.getBalance());
    }
}
```

**Output:**
```
Insufficient funds for withdrawal of 100. Waiting...
Deposited: 150, New Balance: 150
Withdrew: 100, New Balance: 50
Final Balance: 50
```

**Explanation:**
- **Lock:** Explicitly controls access to the `balance` variable.
- **Condition (`sufficientFunds`):** Allows the withdrawal thread to wait until sufficient funds are available.
- **Flow:**
  - The withdrawal thread attempts to withdraw 100 but finds the balance insufficient and waits.
  - After a 2-second delay, the deposit thread deposits 150 and signals the condition.
  - The withdrawal thread resumes, completes the withdrawal, and the final balance is displayed.

**Key Points:**
- **`Lock` Interface:** Offers more flexibility than `synchronized`, such as the ability to try locking without blocking indefinitely.
- **`Condition` Interface:** Facilitates communication between threads, allowing threads to wait for specific conditions to be met.

---

### **3. Concurrent Data Structures**

Java provides a set of thread-safe data structures in the `java.util.concurrent` package. These structures are designed to handle concurrent access without the need for explicit synchronization, enhancing performance and simplifying code.

#### **3.1 ConcurrentHashMap**

**Overview:**
`ConcurrentHashMap` is a thread-safe variant of `HashMap` that allows concurrent read and write operations. It achieves high throughput by partitioning the map into segments, reducing contention among threads.

**Java Implementation:**

```java
import java.util.concurrent.ConcurrentHashMap;

public class ConcurrentHashMapExample {
    public static void main(String[] args) {
        // Create a ConcurrentHashMap
        ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();

        // Runnable task to add key-value pairs
        Runnable writerTask = () -> {
            for (int i = 0; i < 1000; i++) {
                map.put("Key" + i, i);
            }
        };

        // Runnable task to read key-value pairs
        Runnable readerTask = () -> {
            for (int i = 0; i < 1000; i++) {
                map.get("Key" + i);
            }
        };

        // Create multiple writer and reader threads
        Thread writer1 = new Thread(writerTask);
        Thread writer2 = new Thread(writerTask);
        Thread reader1 = new Thread(readerTask);
        Thread reader2 = new Thread(readerTask);

        // Start the threads
        writer1.start();
        writer2.start();
        reader1.start();
        reader2.start();

        // Wait for threads to finish
        try {
            writer1.join();
            writer2.join();
            reader1.join();
            reader2.join();
        } catch (InterruptedException e) {
            System.out.println("Threads interrupted.");
        }

        // Display the size of the map
        System.out.println("Map Size: " + map.size());
        // Expected Output: Map Size: 1000
    }
}
```

**Output:**
```
Map Size: 1000
```

**Explanation:**
- **Concurrent Access:** Multiple writer and reader threads can access the `ConcurrentHashMap` simultaneously without causing data corruption.
- **Performance:** `ConcurrentHashMap` provides better performance in multi-threaded environments compared to synchronized `HashMap`.

**Key Points:**
- **Thread Safety:** Automatically handles synchronization internally.
- **High Throughput:** Designed for high concurrency with minimal contention.
- **Non-blocking Reads:** Reads do not block writes, allowing greater scalability.

---

#### **3.2 BlockingQueue**

**Overview:**
`BlockingQueue` is a thread-safe queue that supports operations that wait for the queue to become non-empty when retrieving elements and wait for space to become available when storing elements. It's commonly used in producer-consumer scenarios.

**Common Implementations:**
- `ArrayBlockingQueue`: Bounded blocking queue backed by an array.
- `LinkedBlockingQueue`: Optionally bounded blocking queue backed by linked nodes.
- `PriorityBlockingQueue`: Unbounded blocking queue that uses priority for ordering.

**Java Implementation:**

```java
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;

class Producer implements Runnable {
    private BlockingQueue<Integer> queue;

    Producer(BlockingQueue<Integer> q) {
        this.queue = q;
    }

    public void run() {
        try {
            for (int i = 1; i <= 5; i++) {
                System.out.println("Producer produced: " + i);
                queue.put(i); // Blocks if the queue is full
                Thread.sleep(500); // Simulate time taken to produce
            }
            queue.put(-1); // Sentinel value to indicate end
        } catch (InterruptedException e) {
            System.out.println("Producer interrupted.");
        }
    }
}

class Consumer implements Runnable {
    private BlockingQueue<Integer> queue;

    Consumer(BlockingQueue<Integer> q) {
        this.queue = q;
    }

    public void run() {
        try {
            while (true) {
                int value = queue.take(); // Blocks if the queue is empty
                if (value == -1)
                    break;
                System.out.println("Consumer consumed: " + value);
                Thread.sleep(1000); // Simulate time taken to consume
            }
        } catch (InterruptedException e) {
            System.out.println("Consumer interrupted.");
        }
    }
}

public class BlockingQueueExample {
    public static void main(String[] args) {
        // Create a LinkedBlockingQueue with capacity 10
        BlockingQueue<Integer> queue = new LinkedBlockingQueue<>(10);

        // Create producer and consumer threads
        Thread producer = new Thread(new Producer(queue));
        Thread consumer = new Thread(new Consumer(queue));

        // Start the threads
        producer.start();
        consumer.start();

        // Wait for threads to finish
        try {
            producer.join();
            consumer.join();
        } catch (InterruptedException e) {
            System.out.println("Main thread interrupted.");
        }

        System.out.println("Producer and Consumer have finished.");
    }
}
```

**Output:**
```
Producer produced: 1
Consumer consumed: 1
Producer produced: 2
Producer produced: 3
Consumer consumed: 2
Producer produced: 4
Producer produced: 5
Consumer consumed: 3
Consumer consumed: 4
Consumer consumed: 5
Producer produced: -1
Producer and Consumer have finished.
```

**Explanation:**
- **Producer Thread:** Produces integers and puts them into the `BlockingQueue`. It signals the end of production by inserting a sentinel value (`-1`).
- **Consumer Thread:** Takes integers from the `BlockingQueue` and processes them. It stops processing when it encounters the sentinel value.
- **Blocking Behavior:** 
  - **`put()` Method:** Blocks if the queue is full.
  - **`take()` Method:** Blocks if the queue is empty.

**Key Points:**
- **Producer-Consumer Model:** Efficiently handles scenarios where producers and consumers operate at different speeds.
- **Thread Safety:** `BlockingQueue` manages synchronization internally, simplifying concurrent programming.
- **Blocking Operations:** Automatically handles waiting and notification between threads.

---

## **Summary and Exercises**

### **Summary:**

In this module, you've learned the essentials of managing multiple threads in Java, ensuring safe access to shared resources through synchronization, and utilizing concurrent data structures to build efficient multi-threaded applications. These skills are crucial for developing responsive and high-performance software that can handle multiple tasks simultaneously.

**Key Takeaways:**
- **Thread Creation:** Understand how to create and manage threads by extending the `Thread` class or implementing the `Runnable` interface.
- **Synchronization:** Learn to synchronize methods and blocks to prevent race conditions and ensure data consistency.
- **Locks and Conditions:** Use `Lock` objects and `Condition` interfaces for advanced thread coordination.
- **Concurrent Data Structures:** Utilize thread-safe data structures like `ConcurrentHashMap` and `BlockingQueue` to simplify concurrent programming.
- **Producer-Consumer Model:** Implement the producer-consumer pattern using `BlockingQueue` for efficient task management between threads.

### **Exercises:**

#### **1. Thread Management:**
- **a. Extending Thread:**
  - **Problem:** Create a program that launches five threads, each printing numbers from 1 to 10 with a short delay between each number.
  - **Task:** Ensure that each thread identifies itself (e.g., "Thread 1: 1", "Thread 2: 1", etc.).
  
- **b. Implementing Runnable:**
  - **Problem:** Implement a `Runnable` that calculates the factorial of a given number and prints the result.
  - **Task:** Create multiple threads to compute factorials of different numbers concurrently.

#### **2. Synchronization and Locks:**
- **a. Synchronized Methods:**
  - **Problem:** Implement a shared counter that can be incremented by multiple threads without causing inconsistencies.
  - **Task:** Compare the results when using synchronized methods versus unsynchronized methods.
  
- **b. Lock Objects and Conditions:**
  - **Problem:** Create a program where one thread prints even numbers and another thread prints odd numbers in sequence up to a specified limit.
  - **Task:** Use `Lock` and `Condition` to synchronize the threads' execution.

#### **3. Concurrent Data Structures:**
- **a. ConcurrentHashMap:**
  - **Problem:** Implement a word frequency counter where multiple threads update the frequency of words in a shared `ConcurrentHashMap`.
  - **Task:** Ensure that the final word counts are accurate after all threads have completed.
  
- **b. BlockingQueue:**
  - **Problem:** Design a logging system where multiple producer threads generate log messages and a single consumer thread writes them to a file.
  - **Task:** Use `BlockingQueue` to manage the log messages efficiently.

#### **4. Combined Techniques:**
- **a. Producer-Consumer with Locks:**
  - **Problem:** Implement a producer-consumer scenario where producers generate data and consumers process it, ensuring thread safety without using `BlockingQueue`.
  - **Task:** Use `Lock` and `Condition` to manage synchronization between producers and consumers.
  
- **b. Multithreaded File Processing:**
  - **Problem:** Create a program that reads a large text file and uses multiple threads to count the occurrence of each word.
  - **Task:** Combine thread management, synchronization, and concurrent data structures to achieve accurate and efficient word counts.

### **Further Reading and Resources:**

- **Books:**
  - *Java Concurrency in Practice* by Brian Goetz.
  - *Effective Java* by Joshua Bloch (Chapters on concurrency).
  - *Head First Java* by Kathy Sierra and Bert Bates (Concurrency chapters).

- **Online Tutorials:**
  - [Java Tutorials: Concurrency](https://docs.oracle.com/javase/tutorial/essential/concurrency/)
  - [GeeksforGeeks: Java Multithreading](https://www.geeksforgeeks.org/multithreading-java/)
  - [Baeldung: Guide to Java Concurrency](https://www.baeldung.com/java-concurrency)

- **Video Lectures:**
  - [Java Multithreading and Concurrency - Udemy](https://www.udemy.com/course/java-multithreading-concurrency-performance-optimization/)
  - [Java Concurrency - Coursera](https://www.coursera.org/learn/java-concurrency)

- **Interactive Platforms:**
  - [LeetCode](https://leetcode.com/) for practicing concurrent programming problems.
  - [HackerRank](https://www.hackerrank.com/domains/tutorials/10-days-of-java) for Java multithreading challenges.
  - [CodeGym](https://codegym.cc/) offers interactive Java courses, including concurrency topics.

---

By completing this module on Concurrency and Multithreading, you've gained a foundational understanding of how to build and manage multi-threaded applications in Java. These skills are vital for developing efficient, responsive, and scalable software systems that can handle multiple tasks simultaneously. Continue practicing through the exercises and explore the provided resources to deepen your expertise in concurrent programming.
