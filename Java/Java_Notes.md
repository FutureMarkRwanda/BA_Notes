# Comprehensive Java Notes for Beginners (Zero to Hero)

These notes are designed for a beginner preparing for an Advanced Java and Object-Oriented Programming (OOP) exam, covering core Java, OOP, Spring Boot, Reactive Programming, Web Services, Servlets, JSP, and Spring Data JPA. They include code examples, comparison tables, and answers to sample review questions for clarity and exam readiness.

## Table of Contents
1. [Introduction to Java](#introduction-to-java)
2. [Java Basics](#java-basics)
3. [Object-Oriented Programming (OOP) Concepts](#object-oriented-programming-oop-concepts)
4. [Advanced Java Concepts](#advanced-java-concepts)
5. [Java Collections Framework](#java-collections-framework)
6. [Exception Handling](#exception-handling)
7. [Multithreading](#multithreading)
8. [File I/O](#file-io)
9. [Java 8+ Features](#java-8-features)
10. [Spring Boot Basics](#spring-boot-basics)
11. [Reactive Programming with Spring WebFlux](#reactive-programming-with-spring-webflux)
12. [Web Services (SOAP and REST)](#web-services-soap-and-rest)
13. [Servlets, JSP, JSTL, and EL](#servlets-jsp-jstl-and-el)
14. [JDBC and Spring Data JPA](#jdbc-and-spring-data-jpa)
15. [Best Practices and Tips](#best-practices-and-tips)

---

## Introduction to Java
Java is a high-level, platform-independent, object-oriented programming language developed by Sun Microsystems (now Oracle) in 1995. It follows the "Write Once, Run Anywhere" (WORA) principle due to the Java Virtual Machine (JVM).

- **Key Features**:
  - Platform-independent
  - Object-oriented
  - Robust (strong memory management, exception handling)
  - Secure
  - Multithreaded
  - Portable

- **Java Editions**:
  
  | Edition | Description |
  |---------|-------------|
  | **Java SE** (Standard Edition) | Core Java for desktop applications |
  | **Java EE** (Enterprise Edition) | For enterprise applications (servlets, JSP, now Jakarta EE) |
  | **Java ME** (Micro Edition) | For mobile and embedded devices |

- **JVM, JRE, JDK**:

  | Term | Description |
  |------|-------------|
  | **JVM** (Java Virtual Machine) | Executes Java bytecode, platform-independent |
  | **JRE** (Java Runtime Environment) | JVM + libraries to run Java applications |
  | **JDK** (Java Development Kit) | JRE + development tools (compiler, debugger) |

---

## Java Basics

### 1. Syntax and Structure
A Java program starts with a `class` and a `main` method, the entry point.

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

- **public**: Access modifier (visible to all)
- **static**: Method belongs to the class, not an instance
- **void**: No return value
- **String[] args**: Command-line arguments
- **Main Method**: Entry point for program execution. Every Java application requires at least one class with a `main` method.

### 2. Variables and Data Types
Java is strongly typed; variables must be declared with a type.

- **Types of Variables**:

  | Type | Description | Scope |
  |------|-------------|------|
  | **Local** | Declared in methods/constructors/blocks | Limited to the block |
  | **Instance** | Declared in a class, non-static | Entire class, tied to an instance |
  | **Static (Class)** | Declared with `static`, belongs to the class | Entire class, accessible via class name |

- **Primitive Types**:

  | Type | Size | Description | Example |
  |------|------|-------------|---------|
  | `byte` | 1 byte | 8-bit integer | `byte b = 127;` |
  | `short` | 2 bytes | 16-bit integer | `short s = 32767;` |
  | `int` | 4 bytes | 32-bit integer | `int i = 1000;` |
  | `long` | 8 bytes | 64-bit integer | `long l = 100000L;` |
  | `float` | 4 bytes | 32-bit floating-point | `float f = 3.14f;` |
  | `double` | 8 bytes | 64-bit floating-point | `double d = 3.14159;` |
  | `char` | 2 bytes | Unicode character | `char c = 'A';` |
  | `boolean` | 1 bit | True/false | `boolean b = true;` |

- **Reference Types**: Objects like `String`, arrays, or custom classes.

```java
String name = "Alice";
int[] numbers = {1, 2, 3};
```

### 3. Operators
- **Arithmetic**: `+`, `-`, `*`, `/`, `%`
- **Relational**: `==`, `!=`, `>`, `<`, `>=`, `<=`
- **Logical**: `&&`, `||`, `!`
- **Bitwise**: `&`, `|`, `^`, `~`, `<<`, `>>`
- **Assignment**: `=`, `+=`, `-=`, etc.

```java
int a = 10, b = 5;
int sum = a + b; // 15
boolean isEqual = (a == b); // false
```

- **== vs equals()**:

  | Operator/Method | Purpose | Example |
  |----------------|---------|--------|
  | `==` | Checks reference equality (same memory location) | `String s1 = new String("A"); String s2 = new String("A"); s1 == s2; // false` |
  | `equals()` | Checks content equality | `s1.equals(s2); // true` |

### 4. Control Flow
- **Conditional Statements**:
  ```java
  int score = 85;
  if (score >= 90) {
      System.out.println("A");
  } else if (score >= 80) {
      System.out.println("B");
  } else {
      System.out.println("C");
  }
  ```

- **Switch Statement**:
  ```java
  int day = 2;
  switch (day) {
      case 1: System.out.println("Monday"); break;
      case 2: System.out.println("Tuesday"); break;
      default: System.out.println("Invalid day"); break;
  }
  ```

- **Loops**:
  ```java
  // For loop
  for (int i = 0; i < 5; i++) {
      System.out.println(i);
  }

  // While loop
  int j = 0;
  while (j < 5) {
      System.out.println(j);
      j++;
  }

  // Do-while loop
  int k = 0;
  do {
      System.out.println(k);
      k++;
  } while (k < 5);
  ```

---

## Object-Oriented Programming (OOP) Concepts

### 1. Classes and Objects
A class is a blueprint for objects. An object is an instance of a class.

```java
class Car {
    String brand;
    int speed;

    void drive() {
        System.out.println(brand + " is driving at " + speed + " mph");
    }
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car();
        car.brand = "Toyota";
        car.speed = 60;
        car.drive(); // Output: Toyota is driving at 60 mph
    }
}
```

- **POJO (Plain Old Java Object)**: A simple Java class with private fields, getters/setters, and no framework-specific dependencies.

### 2. Encapsulation
Encapsulation hides data using `private` fields and exposes methods (getters/setters).

```java
class Person {
    private String name;
    private int age;

    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public int getAge() { return age; }
    public void setAge(int age) { this.age = age; }
}

public class Main {
    public static void main(String[] args) {
        Person person = new Person();
        person.setName("Alice");
        person.setAge(25);
        System.out.println(person.getName() + " is " + person.getAge());
    }
}
```

### 3. Inheritance
Inheritance allows a class to inherit from another using `extends`. Java supports single, multilevel, and hierarchical inheritance (but not multiple inheritance for classes).

```java
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Woof!");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat(); // Inherited method
        dog.bark(); // Dog's method
    }
}
```

- **Types of Inheritance**:

  | Type | Description | Example |
  |------|-------------|---------|
  | **Single** | One class inherits from another | `class Dog extends Animal` |
  | **Multilevel** | Class inherits from a class that inherits from another | `class Puppy extends Dog extends Animal` |
  | **Hierarchical** | Multiple classes inherit from one class | `class Cat extends Animal`, `class Dog extends Animal` |

- **Multiple Inheritance**: Achieved using interfaces, as classes cannot extend multiple classes.
  ```java
  interface B {}
  interface C extends B {}
  interface D {}
  class E extends A implements C, D {}
  ```

- **Super Keyword**:

  | Use | Description | Example |
  |-----|-------------|---------|
  | Access parent field | `super.field` | `super.model` |
  | Call parent method | `super.method()` | `super.print()` |
  | Call parent constructor | `super(args)` | `super(model, price)` |

  ```java
  class Car {
      String model;
      int price;
      Car(String model, int price) {
          this.model = model;
          this.price = price;
      }
      void print() {
          System.out.println("From Parent class");
      }
  }

  class Toyota extends Car {
      int version;
      Toyota(String model, int price, int version) {
          super(model, price);
          this.version = version;
      }
      void print() {
          super.print();
          System.out.println("Print from Toyota: " + super.model);
      }
  }
  ```

### 4. Polymorphism
Polymorphism allows methods to behave differently based on the object.

- **Method Overloading** (Compile-time):
  ```java
  class Calculator {
      int add(int a, int b) { return a + b; }
      double add(double a, double b) { return a + b; }
  }
  ```

- **Method Overriding** (Runtime):
  ```java
  class Animal {
      void sound() {
          System.out.println("Some sound");
      }
  }

  class Cat extends Animal {
      @Override
      void sound() {
          System.out.println("Meow");
      }
  }
  ```

- **Upcasting and Downcasting**:
  ```java
  class Person {}
  class Student extends Person {}

  public class Main {
      public static void main(String[] args) {
          Person p1 = new Student(); // Upcasting (implicit)
          Student s1 = (Student) p1; // Downcasting (explicit)
      }
  }
  ```

### 5. Abstraction
Hides implementation details using abstract classes or interfaces.

- **Abstract Class**:
  ```java
  abstract class Shape {
      abstract double area();
  }

  class Circle extends Shape {
      double radius;
      Circle(double radius) { this.radius = radius; }
      @Override
      double area() { return Math.PI * radius * radius; }
  }
  ```

- **Interface**:
  ```java
  interface Vehicle {
      void start();
      void stop();
      default void show() { System.out.println("Default method"); }
      static void move(int speed) { System.out.println("Speed: " + speed); }
  }

  class Bike implements Vehicle {
      public void start() { System.out.println("Bike starts"); }
      public void stop() { System.out.println("Bike stops"); }
  }
  ```

- **Abstract Class vs Interface**:

  | Feature | Abstract Class | Interface |
  |---------|----------------|-----------|
  | **Methods** | Abstract and concrete | Abstract, default, static (Java 8+) |
  | **Inheritance** | Single | Multiple |
  | **Fields** | Instance fields | Constants (`static final`) |
  | **Access Modifiers** | Any | Public (default) |
  | **Instantiation** | Cannot instantiate | Cannot instantiate |

- **Abstraction vs Encapsulation**:

  | Concept | Description | Example |
  |---------|-------------|---------|
  | **Abstraction** | Hides implementation details, shows only necessary parts | Abstract class/interface |
  | **Encapsulation** | Hides data, provides access via methods | Private fields with getters/setters |

---

## Advanced Java Concepts

### 1. Packages
Organize classes and avoid naming conflicts.

```java
package com.example;

public class MyClass {
    public void sayHello() {
        System.out.println("Hello from package!");
    }
}
```

### 2. Access Modifiers
Control visibility of class members.

| Modifier | Class | Package | Subclass | World |
|----------|-------|---------|----------|-------|
| `public` | Yes | Yes | Yes | Yes |
| `protected` | Yes | Yes | Yes | No |
| `default` | Yes | Yes | No | No |
| `private` | Yes | No | No | No |

### 3. Static Keyword
Used for class-level members.

```java
class Counter {
    static int count = 0;
    Counter() { count++; }
}
```

### 4. Final Keyword
- `final` variable: Constant
- `final` method: Cannot be overridden
- `final` class: Cannot be extended

```java
final class Immutable {
    final int value = 10;
}
```

### 5. equals() and hashCode()
- **equals()**: Checks logical equality.
- **hashCode()**: Returns an integer for hash-based collections.
- **Contract**: If `x.equals(y)`, then `x.hashCode() == y.hashCode()`.

```java
class Student {
    private int id;
    private String name;

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return id == student.id && Objects.equals(name, student.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(id, name);
    }
}
```

### 6. toString()
Provides a string representation of an object.

```java
class Student {
    private int id;
    private String name;

    @Override
    public String toString() {
        return "Student [id=" + id + ", name=" + name + "]";
    }
}
```

### 7. Singleton Pattern
Ensures a class has only one instance.

```java
class StudentService {
    private static StudentService onlyOneInstance;
    private StudentService() {}
    public static StudentService getInstance() {
        if (onlyOneInstance == null) {
            onlyOneInstance = new StudentService();
        }
        return onlyOneInstance;
    }
}

public class Main {
    public static void main(String[] args) {
        StudentService s = StudentService.getInstance();
    }
}
```

---

## Java Collections Framework
Provides data structures for data manipulation.

- **Key Interfaces**:

  | Interface | Description |
  |-----------|-------------|
  | `List` | Ordered, allows duplicates (e.g., `ArrayList`, `LinkedList`) |
  | `Set` | No duplicates (e.g., `HashSet`, `TreeSet`) |
  | `Map` | Key-value pairs (e.g., `HashMap`, `TreeMap`) |

- **Example**:
  ```java
  import java.util.*;

  public class Main {
      public static void main(String[] args) {
          List<String> list = new ArrayList<>();
          list.add("Apple");
          list.add("Banana");
          System.out.println(list); // [Apple, Banana]

          Set<String> set = new TreeSet<>();
          set.add("Apple");
          set.add("Apple"); // Duplicate ignored
          System.out.println(set); // [Apple]

          Map<Integer, String> map = new HashMap<>();
          map.put(1, "Alice");
          map.put(2, "Bob");
          System.out.println(map); // {1=Alice, 2=Bob}
      }
  }
  ```

- **Sorting with Comparable**:
  ```java
  class Employee implements Comparable<Employee> {
      private String lastName, firstName, position;
      private int age, salary;

      public Employee(String lastName, String firstName, String position, int age, int salary) {
          this.lastName = lastName;
          this.firstName = firstName;
          this.position = position;
          this.age = age;
          this.salary = salary;
      }

      @Override
      public int compareTo(Employee o) {
          if (!this.lastName.equals(o.lastName)) return this.lastName.compareTo(o.lastName);
          if (!this.firstName.equals(o.firstName)) return this.firstName.compareTo(o.firstName);
          if (!this.position.equals(o.position)) return this.position.compareTo(o.position);
          if (this.age != o.age) return Integer.compare(this.age, o.age);
          return Integer.compare(this.salary, o.salary);
      }

      @Override
      public String toString() {
          return "Employee [lastName=" + lastName + ", firstName=" + firstName + ", position=" + position + ", age=" + age + ", salary=" + salary + "]";
      }
  }

  public class Main {
      public static void main(String[] args) {
          TreeSet<Employee> emps = new TreeSet<>();
          emps.add(new Employee("Mugisha", "Mike", "Software Engineer", 20, 3000));
          emps.add(new Employee("Mugisha", "Marc", "Database Administrator", 18, 2000));
          emps.add(new Employee("Mugisha", "Mike", "Software Engineer", 20, 3000)); // Duplicate
          emps.add(new Employee("Iradukunda", "Sandra", "Database Administrator", 20, 3000));
          for (Employee emp : emps) {
              System.out.println(emp);
          }
      }
  }
  ```

---

## Exception Handling
Handles runtime errors.

- **Types**:

  | Type | Description | Examples |
  |------|-------------|---------|
  | **Checked** | Must be handled/declared | `IOException`, `FileNotFoundException` |
  | **Unchecked** | Runtime exceptions | `ArithmeticException`, `NullPointerException` |

- **Try-Catch**:
  ```java
  public class Division {
      static void division(int a, int b) {
          try {
              System.out.println(a + "/" + b + "=" + a / b);
          } catch (ArithmeticException e) {
              System.out.println("Exception: " + e.getMessage());
          } finally {
              System.out.println("After try-catch");
          }
      }

      public static void main(String[] args) {
          division(10, 0); // Exception: / by zero
      }
  }
  ```

- **NullPointerException Example**:
  ```java
  public class Program {
      public static void main(String[] args) {
          Student s = null;
          try {
              System.out.println("Length: " + s.getFname());
          } catch (NullPointerException e) {
              System.out.println("Exception: Null object");
          } finally {
              System.out.println("Something");
          }
      }
  }
  ```

---

## Multithreading
Supports concurrent execution.

- **Creating Threads**:
  ```java
  class MyThread extends Thread {
      public void run() { System.out.println("Thread running"); }
  }

  class MyRunnable implements Runnable {
      public void run() { System.out.println("Runnable running"); }
  }

  public class Main {
      public static void main(String[] args) {
          new MyThread().start();
          new Thread(new MyRunnable()).start();
      }
  }
  ```

- **Synchronization**:
  ```java
  class Counter {
      int count = 0;
      synchronized void increment() { count++; }
  }
  ```

---

## File I/O
Classes for file operations.

- **Reading/Writing Files**:
  ```java
  import java.io.*;

  public class CopyLines {
      public static void main(String[] args) throws IOException {
          try (BufferedReader input = new BufferedReader(new FileReader("input.txt"));
               PrintWriter output = new PrintWriter(new FileWriter("output.txt"))) {
              String line;
              while ((line = input.readLine()) != null) {
                  output.println(line);
              }
          }
      }
  }
  ```

---

## Java 8+ Features

### 1. Lambda Expressions
Enable functional programming.

```java
import java.util.Arrays;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob");
        names.forEach(name -> System.out.println(name));
    }
}
```

### 2. Stream API
Process collections functionally.

```java
import java.util.Arrays;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
        numbers.stream()
               .filter(n -> n % 2 == 0)
               .map(n -> n * 2)
               .forEach(System.out::println); // Prints 4, 8
    }
}
```

### 3. Optional
Avoids `NullPointerException`.

```java
import java.util.Optional;

public class Main {
    public static void main(String[] args) {
        Optional<String> name = Optional.ofNullable(null);
        System.out.println(name.orElse("Unknown")); // Prints Unknown
    }
}
```

---

## Spring Boot Basics
Spring Boot simplifies development of stand-alone, production-grade applications.

- **Key Features**:
  - Auto-configuration
  - Embedded servers (Tomcat, Jetty)
  - Starter dependencies
  - Actuator for monitoring

- **Example Application**:
  ```java
  import org.springframework.boot.SpringApplication;
  import org.springframework.boot.autoconfigure.SpringBootApplication;

  @SpringBootApplication
  public class Application {
      public static void main(String[] args) {
          SpringApplication.run(Application.class, args);
      }
  }
  ```

- **REST Controller**:
  ```java
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.RestController;

  @RestController
  public class HelloController {
      @GetMapping("/hello")
      public String sayHello() {
          return "Hello, Spring Boot!";
      }
  }
  ```

- **Dependency Injection**:
  ```java
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.stereotype.Service;
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.RestController;

  @Service
  class MyService {
      String getMessage() { return "Hello from Service!"; }
  }

  @RestController
  class MyController {
      @Autowired
      private MyService myService;

      @GetMapping("/message")
      String getMessage() { return myService.getMessage(); }
  }
  ```

- **@SpringBootApplication**: Enables auto-configuration, component scanning, and configuration properties.

- **Spring Boot Starter**: Aggregates libraries for specific tasks (e.g., `spring-boot-starter-web`).

- **Actuator**: Provides monitoring, metrics, and health checks.

---

## Reactive Programming with Spring WebFlux
Handles asynchronous, non-blocking operations using Project Reactor (`Mono`, `Flux`).

- **Example**:
  ```java
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.RestController;
  import reactor.core.publisher.Flux;
  import java.time.Duration;

  @RestController
  public class UserController {
      @GetMapping("/users")
      Flux<String> getUsers() {
          return Flux.just("Alice", "Bob").delayElements(Duration.ofSeconds(1));
      }
  }
  ```

- **WebClient**:
  ```java
  import org.springframework.web.reactive.function.client.WebClient;
  import reactor.core.publisher.Mono;

  public class Main {
      public static void main(String[] args) {
          WebClient client = WebClient.create("http://localhost:8080");
          Mono<String> response = client.get().uri("/users").retrieve().bodyToMono(String.class);
          response.subscribe(System.out::println);
      }
  }
  ```

---

## Web Services (SOAP and REST)

- **Web Service**: Software that uses standardized protocols (XML/JSON) over the web, self-contained and modular.
- **SOAP**: Uses XML for message exchange, strict format.
- **REST**: Uses HTTP verbs (GET, POST, PUT, DELETE), typically JSON.

- **REST Endpoints**:

  | Verb | Endpoint | Description |
  |------|----------|-------------|
  | POST | `/employees` | Create a new employee |
  | GET | `/employees` | Retrieve all employees |
  | GET | `/employees/{id}` | Retrieve employee by ID |
  | PUT | `/employees/{id}` | Update employee by ID |
  | DELETE | `/employees/{id}` | Delete employee by ID |

- **SOAP vs REST**:

  | Feature | SOAP | REST |
  |---------|------|------|
  | **Protocol** | XML-based | HTTP-based |
  | **Format** | Strict XML | Flexible (JSON, XML) |
  | **State** | Stateless/Stateful | Stateless |
  | **Use Case** | Enterprise, high security | Web APIs, simplicity |

- **XSD in SOAP**: XML Schema Definition validates XML structure and content.

- **Request vs Response**:
  - **Request**: Input to a web service.
  - **Response**: Output from a web service.

- **JSON for POST**:
  ```json
  {
      "id": 1,
      "lastname": "Ange",
      "firstname": "Mugisha",
      "email": "amugisha@domain.com",
      "gender": "Male",
      "dob": "2000-02-30"
  }
  ```

---

## Servlets, JSP, JSTL, and EL

- **Servlet**: Java class extending `HttpServlet` for dynamic web applications.
  ```java
  import jakarta.servlet.http.*;
  import java.io.*;

  public class MyServlet extends HttpServlet {
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
          response.setContentType("text/html");
          PrintWriter out = response.getWriter();
          out.println("<h1>Hello, Servlet!</h1>");
      }
  }
  ```

- **JSP (Jakarta Server Pages)**: HTML with embedded Java code.
  ```jsp
  <%@ page language="java" contentType="text/html" %>
  <html>
  <body>
      <h1>Hello, JSP!</h1>
      <% out.println("Time: " + new java.util.Date()); %>
  </body>
  </html>
  ```

- **EL (Expression Language)**: Simplifies access to data in JSP (`${variable}`).
- **JSTL (JSP Standard Tag Library)**: Provides tags for iteration, conditionals, etc.

- **Example (Servlet + JSP)**:
  ```java
  import jakarta.servlet.*;
  import jakarta.servlet.http.*;
  import java.util.*;

  public class MainController extends HttpServlet {
      protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
          List<Student> students = new ArrayList<>();
          students.add(new Student(1, "Mary", "mary@gmail.com"));
          students.add(new Student(2, "Keza", "keza@gmail.com"));
          request.setAttribute("students", students);
          request.getRequestDispatcher("WEB-INF/student.jsp").forward(request, response);
      }
  }
  ```

  ```jsp
  <%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
  <%@ taglib prefix="c" uri="jakarta.tags.core" %>
  <!DOCTYPE html>
  <html>
  <head>
      <meta charset="UTF-8">
      <title>Display Students</title>
      <style>
          table, th, td { border: 1px solid black; }
          table { border-collapse: collapse; font-size: 2em; }
      </style>
  </head>
  <body>
      <h2>Getting a list of students</h2>
      <table>
          <tr><th>ID</th><th>NAME</th><th>Email</th></tr>
          <c:forEach var="student" items="${students}">
              <tr>
                  <td>${student.code}</td>
                  <td>${student.name}</td>
                  <td>${student.email}</td>
              </tr>
          </c:forEach>
      </table>
  </body>
  </html>
  ```

- **<%= %> vs <% out.print() %>**:

  | Expression | Description |
  |------------|-------------|
  | `<%= %>` | JSP expression, shorthand for printing |
  | `<% out.print() %>` | Scriptlet, explicit print method |

- **Session Management**: Uses `HttpSession` to maintain client state across requests.

---

## JDBC and Spring Data JPA

- **JDBC (Java Database Connectivity)**:
  - Connects Java to databases.
  - **Role of Driver**: Converts Java requests to database-specific protocols.
  - **Driver Types**: JDBC-ODBC Bridge, Native, Network Protocol, Thin Driver.

  ```java
  import java.sql.*;

  public class DatabaseConnection {
      public static void main(String[] args) {
          String url = "jdbc:mysql://localhost:3306/misdb";
          String username = "root";
          String password = "code@2020";
          String driver = "com.mysql.cj.jdbc.Driver";
          try {
              Class.forName(driver);
              Connection con = DriverManager.getConnection(url, username, password);
              Statement st = con.createStatement();
              ResultSet rs = st.executeQuery("SELECT * FROM students");
              while (rs.next()) {
                  System.out.println(rs.getString("name"));
              }
              con.close();
          } catch (Exception e) {
              System.out.println(e);
          }
      }
  }
  ```

- **ResultSet**: Represents query results, provides methods like `getString()`, `getInt()`.

- **JPA (Java Persistence API)**: Specification for ORM.
- **Hibernate**: JPA implementation, maps Java classes to database tables.

- **JPA vs Hibernate**:

  | Feature | JPA | Hibernate |
  |---------|-----|-----------|
  | **Type** | Specification | Implementation |
  | **Flexibility** | Defines interfaces | Provides concrete ORM |
  | **Queries** | JPQL | JPQL + HQL |
  | **Features** | Basic ORM | Advanced caching, lazy loading |

- **Spring Data JPA**:
  - Simplifies database access.
  - **Features**: No-code repositories, reduced boilerplate, generated queries.

- **Student Entity**:
  ```java
  import jakarta.persistence.*;

  @Entity(name = "Student")
  public class Student {
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      @Column(name = "id", nullable = false)
      private Long id;

      @Column(name = "firstName", nullable = false, length = 100)
      private String firstName;

      @Column(name = "lastName", nullable = false, length = 50)
      private String lastName;

      @Column(name = "email", length = 100, unique = true)
      private String email;

      @Column(name = "age", nullable = false)
      private int age;

      public Student() {}
      public Student(String firstName, String lastName, String email, int age) {
          this.firstName = firstName;
          this.lastName = lastName;
          this.email = email;
          this.age = age;
      }

      @Override
      public String toString() {
          return "Student [id=" + id + ", firstName=" + firstName + ", lastName=" + lastName + ", email=" + email + ", age=" + age + "]";
      }
  }
  ```

- **Student Repository**:
  ```java
  import org.springframework.data.jpa.repository.JpaRepository;
  import org.springframework.data.jpa.repository.Query;
  import org.springframework.data.repository.query.Param;
  import java.util.List;

  public interface StudentRepository extends JpaRepository<Student, Integer> {
      @Query("SELECT s FROM Student s WHERE s.email = ?1")
      Student getStudentByEmail(String email);

      @Query(value = "SELECT * FROM student WHERE firstName = :firstName AND age = :age", nativeQuery = true)
      List<Student> findByFirstNameAndAge(@Param("firstName") String firstName, @Param("age") int age);

      List<Student> findByLastName(@Param("lastName") String lastName);
  }
  ```

- **JpaRepository Methods**:

  | Method | Purpose |
  |--------|---------|
  | `save(S entity)` | Saves or updates an entity |
  | `findById(ID id)` | Retrieves entity by ID |
  | `findAll()` | Retrieves all entities |
  | `deleteById(ID id)` | Deletes entity by ID |
  | `count()` | Returns entity count |

- **@JoinColumn**: Specifies foreign key column in relationships.
- **@Transient**: Excludes a field from persistence.
- **Lazy vs Eager Fetching**:

  | Type | Description | Use Case |
  |------|-------------|----------|
  | **Lazy** | Loads data only when accessed | Large related data, not always needed |
  | **Eager** | Loads data immediately | Small data, always needed |

---

## Best Practices and Tips
- Use meaningful names for variables/classes.
- Follow naming conventions (`camelCase`, `PascalCase`).
- Handle exceptions appropriately.
- Use generics in collections.
- Avoid excessive `static` usage.
- Use Spring Boot starters and auto-configuration.
- In reactive programming, manage backpressure.
- Comment code clearly.
- Override `equals()`, `hashCode()`, and `toString()` for custom objects.

---