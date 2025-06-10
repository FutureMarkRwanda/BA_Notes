# Unit 11: Object-Oriented Programming and Java

## 11.1 Classes vs Objects in Java
Classes and objects are fundamental to Java’s object-oriented programming (OOP) approach, defining structure and instances, respectively.

- **What is a Class?**
  - A class is a blueprint or template that defines the properties (data) and behaviors (methods) of objects.
  - It specifies what an object can store and do but doesn’t hold actual data itself.
  - Syntax: `class ClassName { // fields, methods }`
- **What is an Object?**
  - An object is an instance of a class, created to hold specific data and perform the class’s methods.
  - Multiple objects can be created from one class, each with its own data.
- **Key Difference**:
  - Class: Defines the structure (like a car design).
  - Object: A specific instance (like a car built from the design).
- **Self-Study Tip**:
  - Think of a class as a cookie cutter (defines shape) and objects as cookies (each with unique decorations but same shape).
- **Example**:
  ```java
  class Student {
      int id; // Field (property)
      String name;
      void display() { // Method (behavior)
          System.out.println("ID: " + id + ", Name: " + name);
      }
  }
  public class Main {
      public static void main(String[] args) {
          Student s1 = new Student(); // Object creation
          s1.id = 1;
          s1.name = "Alice";
          s1.display(); // Output: ID: 1, Name: Alice
          Student s2 = new Student(); // Another object
          s2.id = 2;
          s2.name = "Bob";
          s2.display(); // Output: ID: 2, Name: Bob
      }
  }
  ```

## 11.2 Constructor in Java
Constructors initialize objects when they are created, setting up initial values for fields.

- **What is a Constructor?**
  - A special method called automatically when an object is created.
  - Has the same name as the class, no return type (not even `void`).
  - Used to initialize fields or perform setup tasks.
- **Types of Constructors**:
  - **Default Constructor**: No parameters, provided automatically if no constructor is defined.
  - **Parameterized Constructor**: Takes parameters to initialize fields.
  - **Copy Constructor**: Initializes an object using another object’s data (less common in Java).
- **Self-Study Tip**:
  - A constructor is like setting up a new phone with default settings (default constructor) or custom settings (parameterized constructor).
- **Example**:
  ```java
  class Car {
      String model;
      int speed;
      // Default constructor
      Car() {
          model = "Unknown";
          speed = 0;
      }
      // Parameterized constructor
      Car(String m, int s) {
          model = m;
          speed = s;
      }
      void display() {
          System.out.println("Model: " + model + ", Speed: " + speed);
      }
  }
  public class Main {
      public static void main(String[] args) {
          Car c1 = new Car(); // Default constructor
          c1.display(); // Output: Model: Unknown, Speed: 0
          Car c2 = new Car("Toyota", 120); // Parameterized constructor
          c2.display(); // Output: Model: Toyota, Speed: 120
      }
  }
  ```

## 11.3 The Use of “new” and “this” Keywords in Java
The `new` and `this` keywords are essential for object creation and referencing within a class.

- **The `new` Keyword**:
  - Allocates memory for a new object on the heap and calls its constructor.
  - Syntax: `ClassName obj = new ClassName();`
  - Example: `Student s = new Student();` creates a `Student` object.
- **The `this` Keyword**:
  - Refers to the current object within a class.
  - Used to distinguish instance variables from parameters with the same name or to call other constructors.
- **Self-Study Tip**:
  - `new` is like ordering a new toy (creates it), and `this` is like pointing to yourself in a conversation to clarify who you’re talking about.
  - Example:
    ```java
    class Person {
        String name;
        int age;
        Person(String name, int age) {
            this.name = name; // this.name refers to instance variable
            this.age = age;
        }
        void display() {
            System.out.println("Name: " + this.name + ", Age: " + this.age);
        }
    }
    public class Main {
        public static void main(String[] args) {
            Person p = new Person("Alice", 25); // new creates object
            p.display(); // Output: Name: Alice, Age: 25
        }
    }
    ```

## 11.4 Arrays in Java
Arrays store multiple values of the same type in a single variable.

- **What is an Array?**
  - A fixed-size collection of elements of the same data type (e.g., `int`, `String`).
  - Elements are accessed by index (starting at 0).
- **Declaring and Initializing**:
  - Syntax: `type[] arrayName = new type[size];`
  - Example: `int[] numbers = new int[3];`
  - Initialize with values: `int[] numbers = {1, 2, 3};`
- **Accessing Elements**:
  - Use index: `arrayName[index]`
- **Self-Study Tip**:
  - An array is like a row of lockers, each holding one item (value) of the same type, accessed by locker number (index).
- **Example**:
  ```java
  public class Main {
      public static void main(String[] args) {
          int[] scores = new int[3]; // Declare array
          scores[0] = 90;
          scores[1] = 85;
          scores[2] = 88;
          for (int i = 0; i < scores.length; i++) {
              System.out.println("Score " + i + ": " + scores[i]);
          }
          // Output: Score 0: 90, Score 1: 85, Score 2: 88
          String[] names = {"Alice", "Bob", "Charlie"};
          System.out.println("First name: " + names[0]); // Output: Alice
      }
  }
  ```

## 11.5 Inheritance in Java
Inheritance allows a class to inherit fields and methods from another class, promoting code reuse.

- **What is Inheritance?**
  - A mechanism where a new (derived/child) class inherits properties from an existing (base/parent) class.
  - Uses the `extends` keyword.
- **Types**:
  - **Single Inheritance**: One class inherits from one parent.
  - **Multilevel Inheritance**: A class inherits from a derived class (e.g., A → B → C).
  - **Hierarchical Inheritance**: Multiple classes inherit from one parent.
  - **Note**: Java does not support multiple inheritance (one class inheriting from multiple parents) directly but uses interfaces.
- **Example**:
  ```java
  class Animal {
      void eat() {
          System.out.println("This animal eats food.");
      }
  }
  class Dog extends Animal {
      void bark() {
          System.out.println("The dog barks.");
      }
  }
  public class Main {
      public static void main(String[] args) {
          Dog d = new Dog();
          d.eat(); // Inherited method, Output: This……

## 11.6 Access Modifiers in Java
Access modifiers control the visibility and accessibility of class members (fields, methods, constructors).

- **What are Access Modifiers?**
  - Keywords that define who can access a class, field, or method.
- **Types**:
  - **public**: Accessible from everywhere.
  - **protected**: Accessible within the same package and in subclasses (even in different packages).
  - **default** (no modifier): Accessible only within the same package (package-private).
  - **private**: Accessible only within the same class.
- **Self-Study Tip**:
  - Access modifiers are like locks on a house. `public` is an open gate, `private` is a locked room, `protected` is a room for family, and `default` is for neighbors.
- **Example**:
  ```java
  class Employee {
      public String name; // Accessible everywhere
      private int salary; // Accessible only in this class
      protected int age; // Accessible in package and subclasses
      String department; // default: Accessible in package
      void setSalary(int s) {
          if (s > 0) salary = s;
      }
      int getSalary() {
          return salary;
      }
  }
  public class Main {
      public static void main(String[] args) {
          Employee e = new Employee();
          e.name = "Alice"; // OK: public
          e.department = "HR"; // OK: default, same package
          e.age = 30; // OK: protected, same package
          // e.salary = 50000; // Error: private
          e.setSalary(50000); // OK: use public method
          System.out.println("Name: " + e.name + ", Salary: " + e.getSalary());
          // Output: Name: Alice, Salary: 50000
      }
  }
  ```

## 11.7 Overloading and Overriding Method in Java
Overloading and overriding enable flexible method usage in Java.

- **Method Overloading**:
  - Defining multiple methods with the same name but different parameters (number, type, or order).
  - Occurs in the same class, resolved at compile time (static polymorphism).
  - Example:
    ```java
    class Calculator {
        int add(int a, int b) {
            return a + b;
        }
        double add(double a, double b) {
            return a + b;
        }
    }
    public class Main {
        public static void main(String[] args) {
            Calculator calc = new Calculator();
            System.out.println(calc.add(2, 3)); // Output: 5
            System.out.println(calc.add(2.5, 3.5)); // Output: 6.0
        }
    }
    ```
- **Method Overriding**:
  - A subclass provides a specific implementation of a method defined in its parent class.
  - Requires same method name, parameters, and return type; uses `@Override` annotation.
  - Resolved at runtime (dynamic polymorphism).
  - Example:
    ```java
    class Animal {
        void sound() {
            System.out.println("Animal makes a sound");
        }
    }
    class Cat extends Animal {
        @Override
        void sound() {
            System.out.println("Cat meows");
        }
    }
    public class Main {
        public static void main(String[] args) {
            Animal a = new Cat(); // Polymorphism
            a.sound(); // Output: Cat meows
        }
    }
    ```
- **Self-Study Tip**:
  - Overloading is like having multiple screwdrivers of different sizes (same name, different uses). Overriding is like redefining how a tool works for a specific task.

## 11.8 Encapsulation in Java
Encapsulation bundles data and methods, protecting data by restricting direct access.

- **What is Encapsulation?**
  - Combining fields and methods in a class and using access modifiers (e.g., `private`) to hide data.
  - Access data via public getter and setter methods for control and validation.
- **Benefits**:
  - Protects data integrity (e.g., prevent invalid values).
  - Hides implementation details, improving maintainability.
- **Self-Study Tip**:
  - Encapsulation is like a safe: only authorized methods (getters/setters) can access or modify the contents (data).
- **Example**:
  ```java
  class BankAccount {
      private double balance; // Private field
      public void setBalance(double b) { // Setter
          if (b >= 0) balance = b;
      }
      public double getBalance() { // Getter
          return balance;
      }
      public void deposit(double amount) {
          if (amount > 0) balance += amount;
      }
  }
  public class Main {
      public static void main(String[] args) {
          BankAccount account = new BankAccount();
          account.setBalance(1000);
          account.deposit(500);
          System.out.println("Balance: " + account.getBalance());
          // Output: Balance: 1500
          // account.balance = -100; // Error: private
      }
  }
  ```

## 11.9 Abstract Class in Java
Abstract classes provide a partial implementation and cannot be instantiated, serving as templates for subclasses.

- **What is an Abstract Class?**
  - A class declared with the `abstract` keyword that may include abstract methods (no implementation) and concrete methods (with implementation).
  - Cannot create objects directly; must be extended by subclasses.
- **Abstract Methods**:
  - Declared with `abstract` keyword, no body (e.g., `abstract void method();`).
  - Subclasses must implement all abstract methods.
- **Self-Study Tip**:
  - An abstract class is like a half-built house plan. It provides some structure (concrete methods) but requires others to complete it (subclasses implement abstract methods).
- **Example**:
  ```java
  abstract class Shape {
      abstract void draw(); // Abstract method
      void display() { // Concrete method
          System.out.println("This is a shape");
      }
  }
  class Circle extends Shape {
      @Override
      void draw() {
          System.out.println("Drawing a circle");
      }
  }
  public class Main {
      public static void main(String[] args) {
          Shape s = new Circle(); // Polymorphism
          s.draw(); // Output: Drawing a circle
          s.display(); // Output: This is a shape
          // Shape s2 = new Shape(); // Error: cannot instantiate
      }
  }
  ```
