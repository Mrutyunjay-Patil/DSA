---
tags: [DSA Java]
title: Course Module 9. System Design Basics
created: '2024-09-17T14:24:52.319Z'
modified: '2024-09-17T14:32:33.503Z'
---

# **Course Module 9. System Design Basics**

**Duration:** 1 Week

System Design is a critical aspect of software engineering that involves creating architectures for complex software systems. Understanding system design principles is essential for building scalable, efficient, and maintainable applications. This module introduces the foundational concepts of system design, ensuring that even those from non-IT backgrounds can grasp and apply these principles effectively.

---

##### **9.1 Scalable System Design Principles**

Scalability is the ability of a system to handle increased load without compromising performance. Designing scalable systems ensures that applications can grow seamlessly as user demand rises.

- **Load Balancing**
  
  **Explanation:**
  
  Load balancing distributes incoming network traffic across multiple servers to ensure no single server becomes a bottleneck. This enhances the responsiveness and availability of applications.
  
  **Example:**
  
  Imagine a popular online store during a sale event. A load balancer directs customer requests to several servers, preventing any single server from being overwhelmed and ensuring smooth browsing and purchasing experiences.
  
  **Key Concepts:**
  
  - **Round Robin:** Distributes requests sequentially to each server.
  - **Least Connections:** Directs traffic to the server with the fewest active connections.
  - **IP Hash:** Uses the client's IP address to determine which server handles the request.
  
- **Caching**
  
  **Explanation:**
  
  Caching stores frequently accessed data in a temporary storage area (cache) to reduce access time and server load.
  
  **Example:**
  
  When you visit a website, images and static content are often cached in your browser. This means that on subsequent visits, the browser can load these elements from the cache instead of fetching them again from the server, speeding up page load times.
  
  **Types of Caching:**
  
  - **Client-Side Caching:** Stored on the user's device (e.g., browser cache).
  - **Server-Side Caching:** Stored on the server or intermediary servers (e.g., Redis, Memcached).
  
- **Data Partitioning and Replication**
  
  **Explanation:**
  
  - **Data Partitioning (Sharding):** Divides a database into smaller, more manageable pieces called shards, each stored on different servers. This improves performance and allows the system to handle more data.
  
  - **Data Replication:** Copies data across multiple servers to ensure data availability and reliability. If one server fails, others can provide the necessary data without interruption.
  
  **Example:**
  
  A social media platform might partition user data based on geographic regions, storing each region's data on different servers. Simultaneously, critical data is replicated across multiple servers to prevent data loss in case of hardware failures.

---

##### **9.2 Design Patterns**

Design patterns are reusable solutions to common software design problems. They provide standardized approaches to designing flexible and maintainable systems.

- **Singleton Pattern**
  
  **Explanation:**
  
  Ensures that a class has only one instance and provides a global point of access to it.
  
  **Example:**
  
  A configuration manager in an application that loads settings from a file. Ensuring only one instance exists prevents inconsistent configurations.
  
  ```java
  public class ConfigurationManager {
      private static ConfigurationManager instance;
      
      private ConfigurationManager() {
          // Load configuration settings
      }
      
      public static synchronized ConfigurationManager getInstance() {
          if (instance == null) {
              instance = new ConfigurationManager();
          }
          return instance;
      }
      
      // Configuration methods
  }
  ```
  
- **Factory Pattern**
  
  **Explanation:**
  
  Provides an interface for creating objects without specifying the exact class of the object that will be created.
  
  **Example:**
  
  A shape factory that creates different shapes (Circle, Square) based on input.
  
  ```java
  public interface Shape {
      void draw();
  }
  
  public class Circle implements Shape {
      public void draw() {
          System.out.println("Drawing Circle");
      }
  }
  
  public class Square implements Shape {
      public void draw() {
          System.out.println("Drawing Square");
      }
  }
  
  public class ShapeFactory {
      public Shape getShape(String shapeType) {
          if (shapeType == null) {
              return null;
          }
          if (shapeType.equalsIgnoreCase("CIRCLE")) {
              return new Circle();
          } else if (shapeType.equalsIgnoreCase("SQUARE")) {
              return new Square();
          }
          return null;
      }
  }
  ```
  
- **Observer Pattern**
  
  **Explanation:**
  
  Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
  
  **Example:**
  
  A news agency (Subject) that notifies subscribed clients (Observers) when new articles are published.
  
  ```java
  public interface Observer {
      void update(String news);
  }
  
  public interface Subject {
      void registerObserver(Observer o);
      void removeObserver(Observer o);
      void notifyObservers();
  }
  
  public class NewsAgency implements Subject {
      private List<Observer> observers = new ArrayList<>();
      private String news;
      
      public void setNews(String news) {
          this.news = news;
          notifyObservers();
      }
      
      public void registerObserver(Observer o) {
          observers.add(o);
      }
      
      public void removeObserver(Observer o) {
          observers.remove(o);
      }
      
      public void notifyObservers() {
          for (Observer o : observers) {
              o.update(news);
          }
      }
  }
  
  public class NewsChannel implements Observer {
      private String news;
      
      public void update(String news) {
          this.news = news;
          System.out.println("NewsChannel received news: " + news);
      }
  }
  ```
  
- **Strategy Pattern**
  
  **Explanation:**
  
  Defines a family of algorithms, encapsulates each one, and makes them interchangeable. It allows the algorithm to vary independently from clients that use it.
  
  **Example:**
  
  A payment processing system that can use different payment strategies (Credit Card, PayPal).
  
  ```java
  public interface PaymentStrategy {
      void pay(int amount);
  }
  
  public class CreditCardPayment implements PaymentStrategy {
      private String cardNumber;
      
      public CreditCardPayment(String cardNumber) {
          this.cardNumber = cardNumber;
      }
      
      public void pay(int amount) {
          System.out.println("Paid " + amount + " using Credit Card: " + cardNumber);
      }
  }
  
  public class PayPalPayment implements PaymentStrategy {
      private String email;
      
      public PayPalPayment(String email) {
          this.email = email;
      }
      
      public void pay(int amount) {
          System.out.println("Paid " + amount + " using PayPal: " + email);
      }
  }
  
  public class ShoppingCart {
      private PaymentStrategy paymentStrategy;
      
      public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
          this.paymentStrategy = paymentStrategy;
      }
      
      public void checkout(int amount) {
          paymentStrategy.pay(amount);
      }
  }
  ```

---

##### **9.3 Database Design Basics**

Databases are essential for storing and managing data in software applications. Understanding the fundamentals of database design ensures efficient data storage, retrieval, and manipulation.

- **SQL vs. NoSQL Databases**
  
  **SQL Databases (Relational Databases):**
  
  - **Structure:** Tables with rows and columns.
  - **Schema:** Fixed schema with predefined data types.
  - **ACID Compliance:** Ensures reliable transactions.
  - **Use Cases:** Banking systems, enterprise applications.
  
  **Example:**
  
  MySQL, PostgreSQL, Oracle Database.
  
  **NoSQL Databases (Non-Relational Databases):**
  
  - **Structure:** Flexible schemas, including key-value pairs, documents, wide-columns, or graphs.
  - **Scalability:** Designed for horizontal scaling.
  - **Use Cases:** Real-time web applications, big data analytics, content management.
  
  **Example:**
  
  MongoDB (Document), Redis (Key-Value), Cassandra (Wide-Column), Neo4j (Graph).
  
  **Choosing Between SQL and NoSQL:**
  
  - **SQL:** When data integrity and complex queries are essential.
  - **NoSQL:** When dealing with large volumes of unstructured data and requiring high scalability.
  
- **Normalization**
  
  **Explanation:**
  
  Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity. It involves dividing large tables into smaller, related tables and defining relationships between them.
  
  **Normal Forms:**
  
  - **First Normal Form (1NF):** Ensures that the table has no repeating groups and each field contains only atomic (indivisible) values.
  
  - **Second Normal Form (2NF):** Achieves 1NF and ensures that all non-key attributes are fully functional dependent on the primary key.
  
  - **Third Normal Form (3NF):** Achieves 2NF and ensures that all the attributes are only dependent on the primary key.
  
  **Example:**
  
  Consider a table storing student information:
  
  | StudentID | StudentName | Course1 | Course2 | Instructor1 | Instructor2 |
  |-----------|-------------|---------|---------|-------------|-------------|
  | 1         | Alice       | Math    | Physics | Dr. Smith   | Dr. Brown   |
  
  **Issues:**
  
  - Redundancy: Instructor names are repeated.
  - Update Anomalies: Changing an instructor's name requires updates in multiple places.
  
  **Normalized Tables:**
  
  **Students Table:**
  
  | StudentID | StudentName |
  |-----------|-------------|
  | 1         | Alice       |
  
  **Courses Table:**
  
  | CourseID | CourseName | InstructorID |
  |----------|------------|--------------|
  | 101      | Math       | 201          |
  | 102      | Physics    | 202          |
  
  **Instructors Table:**
  
  | InstructorID | InstructorName |
  |--------------|-----------------|
  | 201          | Dr. Smith       |
  | 202          | Dr. Brown       |
  
  **Benefits:**
  
  - Eliminates redundancy.
  - Simplifies updates and maintenance.
  - Enhances data integrity.

---

##### **9.4 Practical System Design Example**

To solidify your understanding, let's walk through designing a simple scalable web application: an online bookstore.

- **Requirements:**
  
  - Users can browse and search for books.
  - Users can add books to a shopping cart and make purchases.
  - The system should handle high traffic during peak times.
  
- **Design Components:**
  
  1. **Frontend:**
     
     - User Interface built with HTML, CSS, JavaScript.
     - Frameworks like React or Angular for dynamic content.
  
  2. **Backend:**
     
     - RESTful APIs built with Java (Spring Boot) or Node.js.
     - Handles user requests, business logic, and data processing.
  
  3. **Database:**
     
     - **SQL Database (e.g., PostgreSQL):** Stores structured data like user profiles, orders.
     - **NoSQL Database (e.g., MongoDB):** Stores product catalog for flexible and fast access.
  
  4. **Load Balancer:**
     
     - Distributes incoming traffic across multiple backend servers to ensure availability.
  
  5. **Caching Layer:**
     
     - **Redis:** Caches frequently accessed data like book details to reduce database load.
  
  6. **Search Engine:**
     
     - **Elasticsearch:** Provides fast and scalable search capabilities for the book catalog.
  
  7. **Payment Gateway Integration:**
     
     - Securely processes user payments through third-party services like Stripe or PayPal.
  
  8. **Content Delivery Network (CDN):**
     
     - Distributes static content globally to reduce latency and improve load times.
  
  9. **Monitoring and Logging:**
     
     - Tools like Prometheus and Grafana for system monitoring.
     - Centralized logging with ELK Stack (Elasticsearch, Logstash, Kibana) for troubleshooting.
  
- **Scalability Considerations:**
  
  - **Horizontal Scaling:** Add more servers to handle increased load.
  - **Database Sharding:** Distribute user and order data across multiple database instances.
  - **Auto-Scaling:** Automatically adjust the number of active servers based on traffic patterns.
  
- **Security Measures:**
  
  - **Authentication and Authorization:** Secure user accounts and access controls.
  - **Data Encryption:** Protect sensitive data both in transit and at rest.
  - **Regular Security Audits:** Identify and mitigate potential vulnerabilities.

---

##### **9.5 Summary and Key Takeaways**

- **Scalability** ensures that systems can handle growth efficiently through load balancing, caching, and data partitioning.
- **Design Patterns** provide reusable solutions to common problems, enhancing code maintainability and flexibility.
- **Database Design** is crucial for data integrity and performance, with normalization reducing redundancy and SQL/NoSQL choices depending on use cases.
- **Practical Application** of these principles through real-world examples reinforces understanding and prepares you for system design interviews.

---

##### **Resources:**

- *"Designing Data-Intensive Applications" by Martin Kleppmann*
- *"System Design Interview – An Insider's Guide" by Alex Xu*
- Coursera Course: *Scalable Web Applications and Systems Design*
- YouTube Playlist: *Gaurav Sen’s System Design Tutorials*
- Online Tool: *Lucidchart* for creating system design diagrams

---

By the end of this module, you will have a solid understanding of the fundamental principles of system design, enabling you to architect scalable and efficient systems. This knowledge is not only essential for technical interviews at top-tier companies like Microsoft and Google but also invaluable for real-world software development.
