1. **What are the main ideas of Object-Oriented Programming (OOP) in Java?**

**Answer:**
Java OOP is based on four ideas:

- **Encapsulation:** Putting data (fields) and methods that work on that data into one place (class) and hiding some details using private, protected, or public keywords.
- **Inheritance:** Creating a new class (child) that uses properties and methods from an existing class (parent), helping to reuse code.
- **Polymorphism:** Letting one interface work for different actions. This happens when methods share the same name (overloading) or when a child class changes the behavior of a parent class method (overriding).
- **Abstraction:** Simplifying complex things by focusing on important parts and hiding the details. This is done using abstract classes and interfaces.

2. **What is the difference between an abstract class and an interface in Java?**

**Answer:**
- **Abstract Class:**
  - Can have methods with code and methods without code.
  - Can have normal variables (that hold state).
  - Can have constructors (but you can't create an instance of an abstract class directly).
  - A class can only extend one other class.
  
- **Interface:**
  - Traditionally, all methods had no code until Java 8, which added default and static methods.
  - Can only have constants (static final variables) by default.
  - No constructors, so you can’t create an interface object directly.
  - A class can implement many interfaces, allowing multiple behaviors.
  - Since Java 8 and 9, interfaces can also include code methods (default, static, and private).

3. **Explain what the Java Virtual Machine (JVM) is and its parts.**

**Answer:**
The JVM is a program that runs Java code on any computer, hiding details about the hardware and OS. Its main parts are:

- **Class Loader:** Loads Java classes into memory.
- **Runtime Data Areas:** Memory areas where Java stores data, like:
  - **Method Area:** Data about classes.
  - **Heap:** Where objects live.
  - **Stack:** Where methods run and store local data.
  - **PC Registers and Native Method Stacks:** For JVM operations and native code.
- **Execution Engine:** Runs the Java code and uses a Just-In-Time (JIT) compiler to turn Java code into machine code.
- **Garbage Collector:** Cleans up memory by removing objects that are no longer used.

4. **What is the difference between == and .equals() in Java?**

**Answer:**
- **== Operator:** 
  - Compares basic types directly.
  - For objects, checks if two references point to the exact same object.

- **.equals() Method:**
  - A method to check if two objects are "logically" equal.
  - By default, it does the same as == unless a class changes it to compare values instead.

Example:
```java
String s1 = new String("test");
String s2 = new String("test");

System.out.println(s1 == s2);      // false because they are different objects
System.out.println(s1.equals(s2)); // true because their content is the same
```

5. **How does Java manage memory and garbage collection?**

**Answer:**
Java automatically manages memory using garbage collection:

- **Heap Memory:** Where all new objects go.
- The garbage collector looks for objects that aren’t used anymore and frees their memory.
- Java uses different garbage collection methods (like Serial, Parallel, G1) and divides memory into parts (young and old generations) to improve efficiency.
- You can suggest garbage collection using `System.gc()`, but the JVM decides when to collect.
- This system helps avoid memory leaks and errors, so you don’t have to manually free memory.

6. **What are exceptions in Java, and how do you deal with them?**

**Answer:**
Exceptions are errors or unusual conditions in a program. Java handles them with:

- **Checked Exceptions:** Must be caught or declared in methods (e.g., IOException).
- **Unchecked Exceptions:** Also known as runtime exceptions (e.g., NullPointerException) that don’t need explicit handling.
- **Error:** Serious problems not meant to be caught by your program.

To handle exceptions, use try/catch/finally:

```java
try {
    // code that might throw an exception
} catch (SpecificException ex) {
    // handle the exception
} finally {
    // code that always runs, like closing resources
}
```

7. **What is the difference between ArrayList and LinkedList in Java?**

**Answer:**
- **ArrayList:**
  - Uses an array internally.
  - Fast access to elements by position.
  - Slower when inserting or deleting elements in the middle because it shifts other elements.
  - Good for many reads and few changes.

- **LinkedList:**
  - Uses a chain of nodes.
  - Slower access by position because it goes through each element one by one.
  - Faster insertions and deletions because it just changes links between nodes.
  - Good for many insertions and removals.

8. **What is multithreading in Java and how do you create a thread?**

**Answer:**
Multithreading means running more than one task at the same time. To create a thread in Java, you can:

- **Extend Thread class:**
  ```java
  public class MyThread extends Thread {
      public void run() {
          // task code here
      }
  }
  MyThread t = new MyThread();
  t.start();
  ```

- **Implement Runnable interface:**
  ```java
  public class MyRunnable implements Runnable {
      public void run() {
          // task code here
      }
  }
  Thread t = new Thread(new MyRunnable());
  t.start();
  ```
Using Runnable is often better because Java only allows one class to be extended.

9. **What are lambda expressions and functional interfaces in Java 8?**

**Answer:**
- **Lambda Expressions:** A shorter way to write code that can be passed around like data, usually used for simple functions. Syntax: `(parameters) -> { code }`.

Example:
```java
List<String> names = Arrays.asList("Alice", "Bob");
names.forEach(name -> System.out.println(name));
```

- **Functional Interfaces:** An interface with exactly one abstract method. They are meant to be used with lambda expressions. Java 8 has built-in ones like Predicate, Function, Consumer, and Supplier.

Example:
```java
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}

Calculator add = (a, b) -> a + b;
System.out.println(add.calculate(5, 3)); // prints 8
```

10. **What is the final keyword in Java used for?**

**Answer:**
- **final variable:** Its value cannot change once set.
- **final method:** Cannot be changed by subclasses.
- **final class:** Cannot be extended (no new subclasses).

Using final can help keep code safe and clear.

11. **What is the difference between JDK, JRE, and JVM?**

**Answer:**
- **JDK (Java Development Kit):** Tools for writing Java programs, like the compiler. It includes the JRE.
- **JRE (Java Runtime Environment):** What you need to run Java programs. It has the JVM and libraries, but no tools to write code.
- **JVM (Java Virtual Machine):** The engine that runs Java programs by turning Java code into machine code.

12. **Explain method overloading and method overriding.**

**Answer:**
- **Method Overloading:** Having several methods with the same name in one class but different parameters. It lets you use the same method name for different tasks.
  
Example:
```java
class MathUtil {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}
```

- **Method Overriding:** A subclass changes how a method from its parent class works. The method signature stays the same.
  
Example:
```java
class Animal {
    void makeSound() { System.out.println("Some sound"); }
}

class Dog extends Animal {
    @Override
    void makeSound() { System.out.println("Bark"); }
}
```

13. **What does the static keyword mean in Java?**

**Answer:**
- **Static Variables:** Belong to the class, not any one object. All objects share the same value.
- **Static Methods:** Can be called without creating an object. They can’t directly use non-static parts of the class.
- **Static Blocks:** Run once when the class loads, often to set up static variables.

Use static for features that should be shared by all objects.

14. **What is the Java Collections Framework and why is it important?**

**Answer:**
The Java Collections Framework is a set of classes and interfaces for working with groups of objects, like lists, sets, and maps. It gives you:

- Standard ways to store and work with groups of objects.
- Ready-made classes like ArrayList, HashSet, HashMap, etc.
- Helpful methods for sorting, searching, and more.

It’s important because it saves time, makes code easier, and makes it simple to switch between different ways of storing data without big changes in code.

15. **What does immutability mean in Java? How do you make a class immutable?**

**Answer:**
Immutability means once an object is made, you cannot change it. Immutable objects are safe to use by many threads at once.

To make a class immutable:
- Mark the class as final to stop others from changing it.
- Make all fields private and final.
- Set all fields only once in the constructor.
- Do not provide any methods that change fields.
- If a field is an object that can change, don’t return it directly—return a copy instead.

Example:
```java
public final class ImmutablePoint {
    private final int x;
    private final int y;

    public ImmutablePoint(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int getX() { return x; }
    public int getY() { return y; }
}
```

16. **What is the difference between HashMap, TreeMap, and LinkedHashMap?**

**Answer:**
They all store key-value pairs but work differently:

- **HashMap:** 
  - Does not keep any order.
  - Fast access for adding and retrieving.
  - Allows one null key and many null values.

- **TreeMap:** 
  - Keeps keys in sorted order.
  - Slower (takes more time) because it sorts keys.
  - Does not allow null keys.

- **LinkedHashMap:** 
  - Keeps keys in the order they were added (or access order if set).
  - Slightly slower than HashMap because it maintains order.
  - Good when you need predictable order.

17. **What are generics in Java and why are they useful?**

**Answer:**
Generics let you write classes and methods that work with any type safely. They help catch errors at compile time and avoid the need to cast objects.

Example:
```java
public class Box<T> {
    private T content;
  
    public void set(T content) { this.content = content; }
    public T get() { return content; }
}

Box<String> stringBox = new Box<>();
stringBox.set("Hello");
String content = stringBox.get();  // No cast needed
```
They make code safer and more flexible.

18. **What is reflection in Java? When would you use it?**

**Answer:**
Reflection lets a program look at and change its own structure while it runs. You can:
- Check what classes, methods, and fields exist.
- Create objects and call methods even if you don’t know their names until run time.

Use reflection in:
- Frameworks (like Spring or Hibernate) to work with classes without knowing them ahead of time.
- Testing tools that need to work with many types of objects.

Be careful: Reflection can slow down your program, make it harder to understand, and break security.

19. **How does Java handle synchronization? What is the difference between synchronized methods and blocks?**

**Answer:**
Java uses synchronization to control access to shared resources by different threads:

- **Synchronized Methods:** Marking an entire method as synchronized means only one thread can use that method on an object at a time.
  ```java
  public synchronized void increment() {
      count++;
  }
  ```
  
- **Synchronized Blocks:** Only part of a method is locked. You can choose a specific object to lock on.
  ```java
  public void increment() {
      synchronized(this) {
          count++;
      }
  }
  ```
  
**Difference:**
- Synchronized methods lock the whole method. Synchronized blocks lock only a piece of code.
- Blocks give more control over what is locked and can use different lock objects.

20. **What are Java streams and how are they different from collections?**

**Answer:**
- **Collections:** Data structures that store and let you manipulate data in memory.
- **Streams:** Tools to process sequences of data from a source (like a collection) without storing them. They focus on what to do with data rather than how to do it.

Differences:
- **Lazy Evaluation:** Stream operations only happen when needed.
- **Functional Style:** Streams use methods like filter, map, and reduce for a functional programming style.
- **Parallel Processing:** Streams can easily run operations in parallel.
- **Immutability:** Streams don’t change the original data; they create new results.

Example:
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
List<String> filteredNames = names.stream()
    .filter(name -> name.startsWith("A"))
    .collect(Collectors.toList());
```

21. **What does the volatile keyword do in Java?**

**Answer:**
The `volatile` keyword tells Java that a variable may be changed by different threads. It makes sure:
- When one thread changes the value, other threads see the change right away.
- The order of reading and writing that variable is kept in order.

Note: `volatile` does not make complex operations atomic. For those, you need synchronization or special classes.

22. **What is a deadlock in Java, and how can you avoid it?**

**Answer:**
A deadlock happens when two or more threads wait forever for each other to release locks. To avoid deadlocks:
- Always lock resources in the same order.
- Use timeouts when trying to get a lock, so you don't wait forever.
- Lock only the small part of code that needs it.
- Use a clear order or hierarchy for locks to reduce conflicts.

23. **What are annotations in Java and how do you use them?**

**Answer:**
Annotations are notes you add to code (like above classes, methods, or fields) that do not change how the code runs by themselves. They can be used by the compiler, tools, or at runtime to add extra behavior. Common ones are:
- `@Override`
- `@Deprecated`
- `@SuppressWarnings`

You can also create your own annotation:
```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface MyAnnotation {
    String value();
}

public class MyClass {
    @MyAnnotation("Test")
    public void myMethod() { }
}
```
Frameworks like Spring use annotations to know how to connect parts of the program.

24. **What does the transient keyword do in serialization?**

**Answer:**
The `transient` keyword tells Java not to save a field when converting an object to a byte stream (serialization). When you load the object again, transient fields get default values. Use `transient` for:
- Sensitive information.
- Data that can be recalculated.
- Data you don’t want to save.

Example:
```java
class User implements Serializable {
    private String username;
    private transient String password; // not saved
}
```

25. **What are design patterns? Can you name some common ones in Java?**

**Answer:**
Design patterns are tried and tested solutions to common programming problems. They are like templates for solving design issues. Common patterns include:

- **Creational Patterns:** How to create objects.
  - Singleton: Only one instance of a class exists.
  - Factory: Create objects without specifying exact class.
  - Builder: Build complex objects step by step.

- **Structural Patterns:** How to combine classes.
  - Adapter: Make incompatible interfaces work together.
  - Decorator: Add responsibilities to objects dynamically.
  - Proxy: Control access to an object.

- **Behavioral Patterns:** How objects communicate.
  - Observer: When one object changes, others are notified.
  - Strategy: Swap out algorithms easily.
  - Command: Encapsulate a request as an object.
