# Unit 7: Object-Oriented Programming in C++

## 7.1 Introduction to Object-Oriented Programming (OOP)
Object-Oriented Programming (OOP) is a programming approach that organizes code around objects, which combine data and behavior, making it easier to model real-world systems.

- **What is OOP?**
  - OOP focuses on creating objects that represent real-world entities (e.g., a car, a student).
  - Each object contains **data** (attributes, like a car’s color) and **functions** (methods, like driving the car).
  - OOP makes code modular, reusable, and easier to maintain.
- **Key Principles of OOP**:
  - **Encapsulation**: Bundling data and methods together, hiding details from the outside.
  - **Abstraction**: Showing only essential features, hiding complexity.
  - **Inheritance**: Allowing one class to inherit properties from another.
  - **Polymorphism**: Enabling objects to be treated as instances of a parent class, with different behaviors.
- **Why Use OOP?**
  - Models real-world problems naturally (e.g., a student management system).
  - Simplifies large projects by breaking them into manageable objects.
  - Promotes code reuse, reducing redundancy.
- **Example**: Think of a `Car` object with attributes (color, speed) and methods (drive, stop). OOP lets you create multiple car objects with different colors but shared behavior.

## 7.2 Class Definition in C++
A class is a blueprint for creating objects, defining their properties (data) and behaviors (methods).

- **What is a Class?**
  - A class defines the structure of an object, like a template.
  - It specifies what data the object holds and what it can do.
- **Syntax**:
  ```cpp
  class ClassName {
  public: // Access specifier (public, private, protected)
      // Data members (variables)
      // Member functions (methods)
  };
  ```
- **Explanation**:
  - `class`: Keyword to define a class.
  - `public`: Members are accessible from outside the class.
  - `private`: Members are accessible only within the class (default if not specified).
- **Example**:
  ```cpp
  #include <iostream>
  #include <string>
  class Student {
  public:
      int id; // Data member
      std::string name;
      void display() { // Member function
          std::cout << "ID: " << id << ", Name: " << name << std::endl;
      }
  };
  int main() {
      Student s1; // Create an object
      s1.id = 1; // Set data
      s1.name = "Alice";
      s1.display(); // Call method, Output: ID: 1, Name: Alice
      return 0;
  }
  ```
- **Self-Study Tip**:
  - Think of a class as a recipe (e.g., for a cake). The recipe lists ingredients (data) and steps (methods). You can use the recipe to make multiple cakes (objects).

## 7.3 Object in C++
An object is an instance of a class, created to use the class’s data and methods.

- **What is an Object?**
  - An object is a specific instance of a class, like a real cake made from the recipe.
  - It has its own copy of the class’s data members and can call its methods.
- **Creating Objects**:
  - Syntax: `ClassName objectName;`
  - Multiple objects can be created from one class, each with different data.
- **Example**:
  ```cpp
  #include <iostream>
  #include <string>
  class Car {
  public:
      std::string model;
      int speed;
      void drive() {
          std::cout << model << " is driving at " << speed << " mph." << std::endl;
      }
  };
  int main() {
      Car car1; // First object
      car1.model = "Toyota";
      car1.speed = 60;
      car1.drive(); // Output: Toyota is driving at 60 mph.
      Car car2; // Second object
      car2.model = "Honda";
      car2.speed = 70;
      car2.drive(); // Output: Honda is driving at 70 mph.
      return 0;
  }
  ```
- **Self-Study Tip**:
  - Imagine objects as individual students created from a `Student` class. Each student has their own ID and name but follows the same behavior (e.g., display info).

## 7.4 Data Encapsulation and Data Abstraction in C++
Encapsulation and abstraction are core OOP principles that protect data and simplify usage.

- **Data Encapsulation**:
  - **Definition**: Bundling data and methods in a class, restricting direct access to data using access specifiers (`private`, `protected`).
  - **Purpose**: Protects data from unauthorized access and modification.
  - **How?** Use `private` for data and provide `public` getter/setter methods.
  - **Example**:
    ```cpp
    #include <iostream>
    #include <string>
    class Employee {
    private:
        int salary; // Private data
    public:
        void setSalary(int s) { // Setter
            if (s > 0) salary = s; // Validation
        }
        int getSalary() { // Getter
            return salary;
        }
    };
    int main() {
        Employee e;
        e.setSalary(50000);
        std::cout << "Salary: " << e.getSalary() << std::endl; // Output: Salary: 50000
        // e.salary = 100; // Error: salary is private
        return 0;
    }
    ```
  - **Self-Study Tip**: Think of encapsulation as locking your valuables in a safe. Only you (via methods) can access or modify them safely.

- **Data Abstraction**:
  - **Definition**: Hiding complex implementation details and showing only essential features to the user.
  - **Purpose**: Simplifies interaction with objects by exposing only necessary methods.
  - **How?** Use classes to hide internal logic and provide simple interfaces.
  - **Example**: A `Phone` class hides how calls are made but provides a `call()` method.
    ```cpp
    #include <iostream>
    class Phone {
    private:
        void connectNetwork() { // Hidden implementation
            std::cout << "Connecting to network..." << std::endl;
        }
    public:
        void call(std::string number) { // Simple interface
            connectNetwork();
            std::cout << "Calling " << number << std::endl;
        }
    };
    int main() {
        Phone p;
        p.call("123-456-7890"); // User only sees this, Output: Connecting to network... Calling 123-456-7890
        return 0;
    }
    ```
  - **Self-Study Tip**: Abstraction is like using a TV remote. You press buttons (methods) without knowing how the TV works internally.

## 7.5 Friend Function in C++
A friend function is a non-member function that can access a class’s private and protected members.

- **What is a Friend Function?**
  - A function declared as `friend` inside a class can access its private/protected data.
  - It’s not a member of the class but has special access privileges.
- **Syntax**:
  ```cpp
  class ClassName {
      friend returnType functionName(parameters);
  };
  ```
- **When to Use?**
  - Useful when external functions need access to private data (e.g., for utility operations).
  - Use sparingly to maintain encapsulation.
- **Example**:
  ```cpp
  #include <iostream>
  class Box {
  private:
      double width;
  public:
      Box(double w) : width(w) {}
      friend void printWidth(Box b); // Friend function declaration
  };
  void printWidth(Box b) {
      std::cout << "Width: " << b.width << std::endl; // Access private member
  }
  int main() {
      Box box(5.5);
      printWidth(box); // Output: Width: 5.5
      return 0;
  }
  ```
- **Self-Study Tip**: Think of a friend function as a trusted outsider who has a key to your house (class) but isn’t a family member (method).

## 7.6 Polymorphism in C++
Polymorphism allows objects of different classes to be treated as objects of a common base class, with different behaviors.

- **What is Polymorphism?**
  - Means “many forms” – objects can behave differently based on their type.
  - Two types:
    - **Compile-Time (Static)**: Achieved via function/operator overloading or templates.
    - **Run-Time (Dynamic)**: Achieved via virtual functions and inheritance.
- **Run-Time Polymorphism Example** (using virtual functions):
  ```cpp
  #include <iostream>
  class Animal {
  public:
      virtual void sound() { // Virtual function
          std::cout << "Some animal sound" << std::endl;
      }
  };
  class Dog : public Animal {
  public:
      void sound() override { // Override base class method
          std::cout << "Woof!" << std::endl;
      }
  };
  int main() {
      Animal* animal = new Dog; // Base class pointer to derived class object
      animal->sound(); // Output: Woof! (Run-time polymorphism)
      delete animal;
      return 0;
  }
  ```
- **Self-Study Tip**: Polymorphism is like a remote control that works for different devices (TV, DVD player). The same button (method) behaves differently depending on the device (class).

## 7.7 Overloading
Overloading allows multiple functions or operators to share the same name but differ in parameters or behavior.

- **Function Overloading**:
  - Define multiple functions with the same name but different parameter lists.
  - Compiler chooses the correct function based on arguments.
  - Example:
    ```cpp
    #include <iostream>
    class Calculator {
    public:
        int add(int a, int b) {
            return a + b;
        }
        double add(double a, double b) {
            return a + b;
        }
    };
    int main() {
        Calculator calc;
        std::cout << calc.add(2, 3) << std::endl; // Output: 5 (int)
        std::cout << calc.add(2.5, 3.5) << std::endl; // Output: 6 (double)
        return 0;
    }
    ```
- **Operator Overloading**:
  - Redefine operators (e.g., `+`, `<<`) for user-defined types.
  - Example:
    ```cpp
    #include <iostream>
    class Point {
    public:
        int x, y;
        Point(int x = 0, int y = 0) : x(x), y(y) {}
        Point operator+(Point p) { // Overload +
            return Point(x + p.x, y + p.y);
        }
    };
    int main() {
        Point p1(1, 2), p2(3, 4);
        Point p3 = p1 + p2; // Uses overloaded +
        std::cout << "x: " << p3.x << ", y: " << p3.y << std::endl; // Output: x: 4, y: 6
        return 0;
    }
    ```
- **Self-Study Tip**: Overloading is like having multiple tools with the same name (e.g., “screwdriver”) but different sizes or types, chosen based on the task.

## 7.8 Constructors and Destructors
Constructors and destructors manage object creation and cleanup.

- **Constructor**:
  - **Definition**: A special member function called when an object is created.
  - Same name as the class, no return type.
  - Types: Default (no parameters), parameterized, copy constructor.
  - Example:
    ```cpp
    #include <iostream>
    #include <string>
    class Student {
    public:
        std::string name;
        int id;
        Student() { // Default constructor
            name = "Unknown";
            id = 0;
        }
        Student(std::string n, int i) { // Parameterized constructor
            name = n;
            id = i;
        }
        void display() {
            std::cout << "ID: " << id << ", Name: " << name << std::endl;
        }
    };
    int main() {
        Student s1; // Default constructor
        s1.display(); // Output: ID: 0, Name: Unknown
        Student s2("Bob", 2); // Parameterized constructor
        s2.display(); // Output: ID: 2, Name: Bob
        return 0;
    }
    ```
- **Destructor**:
  - **Definition**: A special member function called when an object is destroyed (e.g., goes out of scope or is deleted).
  - Name: `~ClassName()`, no parameters, no return type.
  - Used for cleanup (e.g., freeing dynamic memory).
  - Example:
    ```cpp
    #include <iostream>
    class Resource {
    public:
        Resource() {
            std::cout << "Resource allocated" << std::endl;
        }
        ~Resource() { // Destructor
            std::cout << "Resource deallocated" << std::endl;
        }
    };
    int main() {
        Resource r; // Output: Resource allocated
        // When r goes out of scope: Resource deallocated
        return 0;
    }
    ```
- **Self-Study Tip**: Constructors are like setting up a new phone (initializing settings), while destructors are like resetting it before disposal (cleaning up).

## 7.9 Inheritance in C++
Inheritance allows a class to inherit properties (data and methods) from another class.

- **What is Inheritance?**
  - A mechanism where a new class (derived/child) inherits features from an existing class (base/parent).
  - Promotes code reuse and hierarchy.
- **Syntax**:
  ```cpp
  class DerivedClass : access_specifier BaseClass {
      // Additional members
  };
  ```
- **Access Specifiers**:
  - `public`: Public and protected members of the base class remain public/protected.
  - `protected`: Public members of the base class become protected.
  - `private`: Public and protected members become private.
- **Types**:
  - **Single Inheritance**: One base class.
  - **Multiple Inheritance**: Multiple base classes.
  - **Multilevel Inheritance**: A chain of inheritance (e.g., A → B → C).
- **Example (Single Inheritance)**:
  ```cpp
  #include <iostream>
  class Animal {
  public:
      void eat() {
          std::cout << "Animal is eating" << std::endl;
      }
  };
  class Dog : public Animal {
  public:
      void bark() {
          std::cout << "Dog is barking" << std::endl;
      }
  };
  int main() {
      Dog d;
      d.eat(); // Inherited from Animal, Output: Animal is eating
      d.bark(); // Dog's own method, Output: Dog is barking
      return 0;
  }
  ```
- **Self-Study Tip**: Inheritance is like a child inheriting traits from a parent. A `Dog` inherits general `Animal` traits (eating) but adds its own (barking).