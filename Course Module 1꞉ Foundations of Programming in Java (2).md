---
tags: [DSA Java]
title: 'Course Module 1: Foundations of Programming in Java'
created: '2024-09-17T13:45:44.894Z'
modified: '2024-09-17T14:31:57.582Z'
---

# Course Module 1: Foundations of Programming in Java

**Duration:** 1 Week

Welcome to the first module of our course designed to equip you with the foundational knowledge of Java programming. This module is structured to ensure that even those from non-IT backgrounds can grasp the concepts effectively. By the end of this week, you'll have a solid understanding of Java basics, object-oriented programming, exception handling, I/O operations, and the Collections Framework—all essential for tackling Data Structures and Algorithms (DSA) problems in top tech companies like Microsoft and Google.

---

## Table of Contents

1. [Java Syntax and Basics](#java-syntax-and-basics)
   - [Variables, Data Types, Operators](#variables-data-types-operators)
   - [Control Flow Statements](#control-flow-statements)
   - [Methods and Scope](#methods-and-scope)
2. [Object-Oriented Programming (OOP) Concepts](#object-oriented-programming-oop-concepts)
   - [Classes and Objects](#classes-and-objects)
   - [Inheritance, Polymorphism, Abstraction, Encapsulation](#inheritance-polymorphism-abstraction-encapsulation)
   - [Interfaces and Abstract Classes](#interfaces-and-abstract-classes)
3. [Exception Handling](#exception-handling)
   - [Try-Catch Blocks](#try-catch-blocks)
   - [Custom Exceptions](#custom-exceptions)
4. [Input/Output (I/O) in Java](#inputoutput-io-in-java)
   - [Reading from Standard Input](#reading-from-standard-input)
   - [File I/O Basics](#file-io-basics)
5. [Generics and Collections Framework](#generics-and-collections-framework)
   - [Lists, Sets, Maps](#lists-sets-maps)
   - [Iterators and Enhanced For-Loop](#iterators-and-enhanced-for-loop)

---

## Java Syntax and Basics

### Variables, Data Types, Operators

**Explanation:**

- **Variables:** Containers for storing data values. In Java, each variable must be declared with a specific data type.

- **Data Types:** 
  - **Primitive Types:** `int`, `double`, `char`, `boolean`, etc.
  - **Reference Types:** Objects and Arrays.

- **Operators:** Symbols that perform operations on variables and values.
  - **Arithmetic Operators:** `+`, `-`, `*`, `/`, `%`
  - **Relational Operators:** `==`, `!=`, `>`, `<`, `>=`, `<=`
  - **Logical Operators:** `&&`, `||`, `!`
  - **Assignment Operators:** `=`, `+=`, `-=`, etc.

**Example:**

```java
public class BasicsExample {
    public static void main(String[] args) {
        // Variables and Data Types
        int number = 10;
        double price = 99.99;
        char grade = 'A';
        boolean isAvailable = true;
        String message = "Hello, Java!";

        // Operators
        int sum = number + 20;
        boolean result = (number > 5) && isAvailable;

        // Output
        System.out.println("Sum: " + sum);
        System.out.println("Result: " + result);
        System.out.println(message);
    }
}
```

**Output:**
```
Sum: 30
Result: true
Hello, Java!
```

**Exercises:**

1. Declare variables of different data types and print their values.
2. Write a program to calculate the area of a circle given its radius.
3. Use relational and logical operators to compare two numbers and print whether the first is greater than the second.

---

### Control Flow Statements

**Explanation:**

Control flow statements dictate the order in which instructions are executed. They allow the program to make decisions and execute code repeatedly.

- **If Statement:** Executes a block of code if a specified condition is true.
- **For Loop:** Repeats a block of code a specified number of times.
- **While Loop:** Repeats a block of code while a specified condition is true.

**Example:**

```java
public class ControlFlowExample {
    public static void main(String[] args) {
        int score = 85;

        // If-Else Statement
        if (score >= 90) {
            System.out.println("Grade: A");
        } else if (score >= 80) {
            System.out.println("Grade: B");
        } else {
            System.out.println("Grade: C");
        }

        // For Loop
        System.out.println("Numbers from 1 to 5:");
        for (int i = 1; i <= 5; i++) {
            System.out.print(i + " ");
        }

        // While Loop
        System.out.println("\nCountdown:");
        int count = 5;
        while (count > 0) {
            System.out.print(count + " ");
            count--;
        }
    }
}
```

**Output:**
```
Grade: B
Numbers from 1 to 5:
1 2 3 4 5 
Countdown:
5 4 3 2 1 
```

**Exercises:**

1. Write a program that determines if a number is even or odd.
2. Use a `for` loop to print the multiplication table of a given number.
3. Implement a `while` loop that prints numbers from 10 down to 1.

---

### Methods and Scope

**Explanation:**

- **Methods:** Blocks of code designed to perform specific tasks. They help in reusing code and improving readability.
  - **Syntax:** 
    ```java
    returnType methodName(parameters) {
        // method body
    }
    ```

- **Scope:** The visibility of variables. Variables declared inside a method are local to that method, while those declared outside are class-level.

**Example:**

```java
public class MethodsExample {
    // Class-level variable
    static int globalCount = 0;

    public static void main(String[] args) {
        int result = add(5, 10);
        System.out.println("Sum: " + result);

        greet("Alice");
        greet("Bob");

        System.out.println("Global Count: " + globalCount);
    }

    // Method to add two numbers
    public static int add(int a, int b) {
        return a + b;
    }

    // Method to greet a user
    public static void greet(String name) {
        globalCount++;
        System.out.println("Hello, " + name + "!");
    }
}
```

**Output:**
```
Sum: 15
Hello, Alice!
Hello, Bob!
Global Count: 2
```

**Exercises:**

1. Create a method that calculates the factorial of a number.
2. Write a method that checks if a string is a palindrome.
3. Implement a method that finds the maximum of three numbers.

---

## Object-Oriented Programming (OOP) Concepts

### Classes and Objects

**Explanation:**

OOP is a programming paradigm based on the concept of "objects", which can contain data and methods. 

- **Class:** A blueprint for creating objects. It defines the properties (attributes) and behaviors (methods) that the objects created from the class will have.
  
- **Object:** An instance of a class. It represents a specific entity with its own state.

**Example:**

```java
// Class Definition
class Car {
    // Attributes
    String color;
    String model;
    int year;

    // Method
    void displayInfo() {
        System.out.println("Model: " + model + ", Color: " + color + ", Year: " + year);
    }
}

public class ClassesObjectsExample {
    public static void main(String[] args) {
        // Creating Objects
        Car car1 = new Car();
        car1.model = "Toyota Camry";
        car1.color = "Red";
        car1.year = 2020;

        Car car2 = new Car();
        car2.model = "Honda Accord";
        car2.color = "Blue";
        car2.year = 2022;

        // Using Methods
        car1.displayInfo();
        car2.displayInfo();
    }
}
```

**Output:**
```
Model: Toyota Camry, Color: Red, Year: 2020
Model: Honda Accord, Color: Blue, Year: 2022
```

**Exercises:**

1. Define a `Person` class with attributes like `name`, `age`, and `gender`. Create objects and display their information.
2. Create a `Book` class with attributes `title`, `author`, and `price`. Include a method to apply a discount to the price.
3. Implement a `Rectangle` class with methods to calculate area and perimeter.

---

### Inheritance, Polymorphism, Abstraction, Encapsulation

**Explanation:**

These are the four pillars of OOP:

1. **Inheritance:** Allows a new class to inherit properties and behaviors from an existing class.
   - **Example:** A `Dog` class inheriting from an `Animal` class.

2. **Polymorphism:** Allows objects to be treated as instances of their parent class rather than their actual class. It enables one interface to be used for a general class of actions.
   - **Example:** A `Animal` reference pointing to a `Dog` object.

3. **Abstraction:** Hides the complex implementation details and shows only the necessary features of an object.
   - **Example:** Using a `List` without knowing its underlying implementation.

4. **Encapsulation:** Bundles the data (attributes) and methods that operate on the data into a single unit or class. It also restricts direct access to some of the object's components.
   - **Example:** Making class variables `private` and providing `public` getter and setter methods.

**Example:**

```java
// Base Class
class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

// Derived Class (Inheritance and Polymorphism)
class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Dog barks");
    }
}

// Abstract Class (Abstraction)
abstract class Shape {
    abstract double area();
}

// Concrete Class
class Circle extends Shape {
    double radius;

    Circle(double radius) {
        this.radius = radius;
    }

    @Override
    double area() {
        return Math.PI * radius * radius;
    }
}

// Encapsulation Example
class BankAccount {
    private double balance;

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if(amount > 0)
            balance += amount;
    }

    public void withdraw(double amount) {
        if(amount > 0 && balance >= amount)
            balance -= amount;
    }
}

public class OOPConceptsExample {
    public static void main(String[] args) {
        // Inheritance and Polymorphism
        Animal myAnimal = new Dog();
        myAnimal.makeSound(); // Outputs: Dog barks

        // Abstraction
        Shape myCircle = new Circle(5);
        System.out.println("Area of Circle: " + myCircle.area());

        // Encapsulation
        BankAccount account = new BankAccount();
        account.deposit(1000);
        account.withdraw(500);
        System.out.println("Account Balance: " + account.getBalance());
    }
}
```

**Output:**
```
Dog barks
Area of Circle: 78.53981633974483
Account Balance: 500.0
```

**Exercises:**

1. Create a base class `Employee` with a method `calculateSalary()`. Derive classes `Manager` and `Developer` that override this method.
2. Implement an abstract class `Vehicle` with an abstract method `move()`. Create subclasses `Car` and `Bicycle` that provide concrete implementations.
3. Design a `Student` class using encapsulation, ensuring that the student's marks cannot be directly modified from outside the class.

---

### Interfaces and Abstract Classes

**Explanation:**

- **Abstract Classes:**
  - Cannot be instantiated.
  - Can contain both abstract methods (without body) and concrete methods (with body).
  - Used when classes share a common structure but have different implementations.

- **Interfaces:**
  - Define a contract that implementing classes must follow.
  - Can contain abstract methods and default methods (since Java 8).
  - A class can implement multiple interfaces, providing a form of multiple inheritance.

**Example:**

```java
// Interface Definition
interface Movable {
    void move();
    default void description() {
        System.out.println("I can move");
    }
}

// Abstract Class
abstract class Animal {
    abstract void eat();

    void breathe() {
        System.out.println("Animal breathes");
    }
}

// Concrete Class implementing Interface and extending Abstract Class
class Dog extends Animal implements Movable {
    @Override
    void eat() {
        System.out.println("Dog eats dog food");
    }

    @Override
    public void move() {
        System.out.println("Dog runs");
    }
}

public class InterfacesAbstractClassesExample {
    public static void main(String[] args) {
        Dog myDog = new Dog();
        myDog.eat();            // From Animal
        myDog.breathe();       // From Animal
        myDog.move();          // From Movable
        myDog.description();   // From Movable Interface
    }
}
```

**Output:**
```
Dog eats dog food
Animal breathes
Dog runs
I can move
```

**Exercises:**

1. Define an interface `Playable` with methods `play()` and `pause()`. Create classes `MusicPlayer` and `VideoPlayer` that implement this interface.
2. Create an abstract class `Appliance` with an abstract method `turnOn()`. Derive classes `WashingMachine` and `Refrigerator` that provide implementations.
3. Design an interface `Drawable` with a method `draw()`. Implement this interface in classes `Circle`, `Rectangle`, and `Triangle`.

---

## Exception Handling

### Try-Catch Blocks

**Explanation:**

Exception handling is a mechanism to handle runtime errors, ensuring the normal flow of the application. 

- **Try Block:** Contains code that might throw an exception.
- **Catch Block:** Handles the exception if one occurs.
- **Finally Block:** Executes code regardless of whether an exception occurred or not (optional).

**Example:**

```java
public class ExceptionHandlingExample {
    public static void main(String[] args) {
        try {
            int[] numbers = {1, 2, 3};
            System.out.println("Element at index 5: " + numbers[5]); // This will throw ArrayIndexOutOfBoundsException
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Error: Tried to access an invalid array index.");
        } finally {
            System.out.println("Execution completed.");
        }

        // Handling division by zero
        try {
            int a = 10;
            int b = 0;
            int result = a / b; // This will throw ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("Error: Division by zero is not allowed.");
        }
    }
}
```

**Output:**
```
Error: Tried to access an invalid array index.
Execution completed.
Error: Division by zero is not allowed.
```

**Exercises:**

1. Write a program that reads two numbers from the user and divides them, handling possible exceptions.
2. Implement a try-catch block to handle `NumberFormatException` when converting a string to an integer.
3. Use a `finally` block to close a resource (e.g., a file) regardless of whether an exception occurred.

---

### Custom Exceptions

**Explanation:**

Custom exceptions allow developers to create their own exception types, providing more meaningful error messages tailored to specific application scenarios.

**Example:**

```java
// Custom Exception Class
class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}

// Class using Custom Exception
class Person {
    private int age;

    public void setAge(int age) throws InvalidAgeException {
        if(age < 0 || age > 150) {
            throw new InvalidAgeException("Age must be between 0 and 150.");
        }
        this.age = age;
    }
}

public class CustomExceptionExample {
    public static void main(String[] args) {
        Person person = new Person();

        try {
            person.setAge(200); // Invalid age
        } catch (InvalidAgeException e) {
            System.out.println("Exception: " + e.getMessage());
        }

        try {
            person.setAge(25); // Valid age
            System.out.println("Age set successfully.");
        } catch (InvalidAgeException e) {
            System.out.println("Exception: " + e.getMessage());
        }
    }
}
```

**Output:**
```
Exception: Age must be between 0 and 150.
Age set successfully.
```

**Exercises:**

1. Create a custom exception `InsufficientFundsException` for a banking application.
2. Implement a `TemperatureException` that is thrown when a temperature exceeds a certain limit.
3. Design a custom exception `InvalidUserInputException` to handle invalid inputs in a user registration system.

---

## Input/Output (I/O) in Java

### Reading from Standard Input

**Explanation:**

Reading input from the user is essential for interactive programs. Java provides the `Scanner` class for parsing primitive types and strings using regular expressions.

**Example:**

```java
import java.util.Scanner;

public class StandardInputExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Reading an integer
        System.out.print("Enter your age: ");
        int age = scanner.nextInt();

        // Reading a double
        System.out.print("Enter your height in meters: ");
        double height = scanner.nextDouble();

        // Reading a string (nextLine to consume the remaining newline)
        scanner.nextLine(); // Consume newline
        System.out.print("Enter your name: ");
        String name = scanner.nextLine();

        // Output
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Height: " + height + " meters");

        scanner.close();
    }
}
```

**Sample Interaction:**
```
Enter your age: 30
Enter your height in meters: 1.75
Enter your name: John Doe
Name: John Doe
Age: 30
Height: 1.75 meters
```

**Exercises:**

1. Write a program that takes a user's full name and prints it in reverse.
2. Create a program that reads five integers from the user and calculates their average.
3. Implement a simple calculator that takes two numbers and an operator (`+`, `-`, `*`, `/`) from the user and displays the result.

---

### File I/O Basics

**Explanation:**

File I/O allows programs to read from and write to files, enabling data persistence.

- **Reading from a File:** Using classes like `FileReader` and `BufferedReader`.
- **Writing to a File:** Using classes like `FileWriter` and `BufferedWriter`.

**Example:**

```java
import java.io.*;

public class FileIOExample {
    public static void main(String[] args) {
        String filePath = "example.txt";

        // Writing to a File
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
            writer.write("Hello, Java File I/O!");
            writer.newLine();
            writer.write("This is the second line.");
            System.out.println("Successfully wrote to the file.");
        } catch (IOException e) {
            System.out.println("An error occurred during writing.");
            e.printStackTrace();
        }

        // Reading from a File
        try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
            String line;
            System.out.println("\nContents of the file:");
            while((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.out.println("An error occurred during reading.");
            e.printStackTrace();
        }
    }
}
```

**Output:**
```
Successfully wrote to the file.

Contents of the file:
Hello, Java File I/O!
This is the second line.
```

**Exercises:**

1. Write a program that copies the contents of one file to another.
2. Implement a program that appends user input to an existing file.
3. Create a program that reads a file and counts the number of words in it.

---

## Generics and Collections Framework

### Lists, Sets, Maps

**Explanation:**

The Collections Framework provides a set of classes and interfaces for storing and manipulating groups of data.

- **List:** An ordered collection that can contain duplicate elements. Common implementations: `ArrayList`, `LinkedList`.
  
- **Set:** An unordered collection that does not allow duplicate elements. Common implementations: `HashSet`, `TreeSet`.
  
- **Map:** An object that maps keys to values, with no duplicate keys. Common implementations: `HashMap`, `TreeMap`.

**Example:**

```java
import java.util.*;

public class CollectionsExample {
    public static void main(String[] args) {
        // List Example
        List<String> fruits = new ArrayList<>();
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Apple"); // Duplicate
        System.out.println("List: " + fruits);

        // Set Example
        Set<String> uniqueFruits = new HashSet<>(fruits);
        System.out.println("Set: " + uniqueFruits);

        // Map Example
        Map<String, Integer> fruitPrices = new HashMap<>();
        fruitPrices.put("Apple", 2);
        fruitPrices.put("Banana", 1);
        fruitPrices.put("Orange", 3);
        System.out.println("Map: " + fruitPrices);

        // Accessing Map Values
        System.out.println("Price of Banana: " + fruitPrices.get("Banana"));
    }
}
```

**Output:**
```
List: [Apple, Banana, Apple]
Set: [Apple, Banana]
Map: {Orange=3, Banana=1, Apple=2}
Price of Banana: 1
```

**Exercises:**

1. Create a `List` of integers, add elements, and find the maximum and minimum values.
2. Implement a `Set` to store unique email addresses and check for duplicates.
3. Use a `Map` to store student names and their corresponding grades. Retrieve and display a specific student's grade.

---

### Iterators and Enhanced For-Loop

**Explanation:**

- **Iterator:** An object that allows traversing through a collection, one element at a time, and optionally removing elements.

- **Enhanced For-Loop (for-each):** A simplified loop for iterating over arrays or collections without using an index.

**Example:**

```java
import java.util.*;

public class IteratorsExample {
    public static void main(String[] args) {
        // Using Iterator with List
        List<String> colors = new ArrayList<>(Arrays.asList("Red", "Green", "Blue", "Yellow"));

        System.out.println("Using Iterator:");
        Iterator<String> iterator = colors.iterator();
        while(iterator.hasNext()) {
            String color = iterator.next();
            System.out.println(color);
            if(color.equals("Green")) {
                iterator.remove(); // Removing "Green" from the list
            }
        }
        System.out.println("List after removal: " + colors);

        // Using Enhanced For-Loop with Set
        Set<Integer> numbers = new HashSet<>(Arrays.asList(1, 2, 3, 4, 5));

        System.out.println("\nUsing Enhanced For-Loop:");
        for(Integer number : numbers) {
            System.out.println(number);
        }

        // Using Enhanced For-Loop with Map
        Map<String, String> capitals = new HashMap<>();
        capitals.put("USA", "Washington D.C.");
        capitals.put("France", "Paris");
        capitals.put("Japan", "Tokyo");

        System.out.println("\nMap Contents:");
        for(Map.Entry<String, String> entry : capitals.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
    }
}
```

**Output:**
```
Using Iterator:
Red
Green
Blue
Yellow
List after removal: [Red, Blue, Yellow]

Using Enhanced For-Loop:
1
2
3
4
5

Map Contents:
USA -> Washington D.C.
France -> Paris
Japan -> Tokyo
```

**Exercises:**

1. Use an `Iterator` to traverse a `List` of strings and remove all strings that start with the letter 'A'.
2. Implement an enhanced for-loop to calculate the sum of all elements in an array of integers.
3. Iterate over a `Map` using an enhanced for-loop and print all key-value pairs where the value meets a certain condition.

---

## Summary

This week, you've been introduced to the essential foundations of Java programming, covering syntax, control structures, object-oriented principles, exception handling, I/O operations, and the Collections Framework. These concepts are critical for building efficient and robust Java applications and are fundamental for solving complex DSA problems in high-profile tech companies.

### Key Takeaways:

- **Java Basics:** Understanding variables, data types, operators, and control flow statements forms the backbone of Java programming.
- **OOP Concepts:** Grasping classes, objects, inheritance, polymorphism, abstraction, and encapsulation is vital for designing scalable and maintainable code.
- **Exception Handling:** Effectively managing errors ensures your programs can handle unexpected scenarios gracefully.
- **I/O Operations:** Mastering file and standard input/output operations allows your programs to interact with users and external data sources.
- **Collections Framework:** Utilizing lists, sets, maps, iterators, and enhanced for-loops enables efficient data management and manipulation.

### Next Steps:

Proceed to the next module where you'll delve deeper into Data Structures and Algorithms, applying the foundational knowledge you've acquired to solve complex problems and prepare for technical interviews at leading companies.

---

# Additional Resources

- **Books:**
  - *Head First Java* by Kathy Sierra and Bert Bates
  - *Effective Java* by Joshua Bloch

- **Online Tutorials:**
  - [Oracle Java Tutorials](https://docs.oracle.com/javase/tutorial/)
  - [W3Schools Java Tutorial](https://www.w3schools.com/java/)

- **Practice Platforms:**
  - [LeetCode](https://leetcode.com/)
  - [HackerRank](https://www.hackerrank.com/domains/java)
  - [CodeSignal](https://codesignal.com/)

---

Feel free to reach out with any questions or clarifications as you progress through the course. Happy coding!
