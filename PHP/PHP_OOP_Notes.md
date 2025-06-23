# PHP Object-Oriented Programming (OOP) Notes

## Definition
- **Object-Oriented Programming (OOP)**: A programming paradigm that organizes code into reusable objects combining data (properties) and behavior (methods). It models real-world entities as objects with attributes and actions.
- **Paradigm**: A fundamental approach to designing and structuring code, guided by specific principles and practices.
- **Core Concept**: OOP wraps data as objects with associated properties, enhancing security and reducing data exposure by controlling access through well-defined interfaces.

## Major Features of OOP in PHP

### Classes and Objects
- **Class**: A blueprint or template defining properties (attributes) and methods (functions) for creating objects.
- **Object**: An instance of a class, created using the `new` keyword.
- **Syntax**:
  ```php
  class MyClass {
      // Properties and methods go here
  }
  $obj = new MyClass;
  ```
- **Example**: Class to display a person's full name.
  ```php
  class Person {
      public $firstName;
      public $lastName;

      public function displayFullName() {
          echo "Full Name: {$this->firstName} {$this->lastName}\n";
      }
  }

  $person = new Person();
  $person->firstName = 'KABANDANA';
  $person->lastName = 'Emmanuel';
  $person->displayFullName(); // Outputs: Full Name: KABANDANA Emmanuel
  ```

### Encapsulation
- **Definition**: Bundling data and methods within a class, controlling access using access modifiers (`public`, `private`, `protected`).
- **Purpose**: Enhances security by hiding internal implementation details and exposing only necessary interfaces.
- **Example**:
  ```php
  class Fruit {
      private $name;
      private $color;

      public function set_name($name) {
          $this->name = $name;
      }

      public function get_name() {
          return $this->name;
      }

      public function set_color($color) {
          $this->color = $color;
      }

      public function get_color() {
          return $this->color;
      }
  }

  $apple = new Fruit();
  $apple->set_name('Apple');
  $apple->set_color('Red');
  echo 'Name: ' . $apple->get_name() . '<br>'; // Outputs: Name: Apple
  echo 'Color: ' . $apple->get_color(); // Outputs: Color: Red
  ```

### Inheritance
- **Definition**: Allows a child class to inherit properties and methods from a parent class, enabling code reuse and extension.
- **Syntax**: Use the `extends` keyword.
- **Example**:
  ```php
  class Vehicle {
      public $brand;

      public function drive() {
          echo "Driving a {$this->brand}\n";
      }
  }

  class Car extends Vehicle {
      public function honk() {
          echo "Beep beep!\n";
      }
  }

  $car = new Car();
  $car->brand = 'Toyota';
  $car->drive(); // Outputs: Driving a Toyota
  $car->honk(); // Outputs: Beep beep!
  ```

### Polymorphism
- **Definition**: Allows objects of different classes to be treated as objects of a common superclass or interface, using method overriding or interfaces.
- **Method Overriding**: A child class provides its own implementation of a parent class method.
- **Example**:
  ```php
  class Animal {
      public function makeSound() {
          echo "Some generic sound\n";
      }
  }

  class Dog extends Animal {
      public function makeSound() {
          echo "Woof!\n";
      }
  }

  $dog = new Dog();
  $dog->makeSound(); // Outputs: Woof!
  ```

### Abstraction
- **Definition**: Hides implementation details, exposing only essential interfaces via abstract classes or interfaces.
- **Abstract Class**: Cannot be instantiated; meant to be extended. Defined with the `abstract` keyword.
- **Interface**: Defines methods that implementing classes must provide, using the `interface` and `implements` keywords.
- **Example (Interface)**:
  ```php
  interface Shape {
      public function calculateArea();
  }

  class Circle implements Shape {
      private $radius;

      public function __construct($radius) {
          $this->radius = $radius;
      }

      public function calculateArea() {
          return pi() * $this->radius * $this->radius;
      }
  }

  $circle = new Circle(5);
  echo $circle->calculateArea(); // Outputs: 78.539816339745
  ```

### Constructors and Destructors
- **Constructor**: Special method (`__construct`) called when an object is created, used for initialization.
- **Destructor**: Special method (`__destruct`) called when an object is no longer referenced, used for cleanup.
- **Example**:
  ```php
  class Example {
      public function __construct() {
          echo "Object created\n";
      }

      public function __destruct() {
          echo "Object destroyed\n";
      }
  }

  $obj = new Example(); // Outputs: Object created
  unset($obj); // Outputs: Object destroyed
  ```

## Access Modifiers
- **Public**: Accessible from anywhere (default).
- **Private**: Accessible only within the class.
- **Protected**: Accessible within the class and its subclasses.
- **Example**:
  ```php
  class Test {
      public $publicVar = "Public";
      private $privateVar = "Private";
      protected $protectedVar = "Protected";

      public function accessVars() {
          echo $this->privateVar; // Accessible within class
      }
  }

  class SubTest extends Test {
      public function accessProtected() {
          echo $this->protectedVar; // Accessible in subclass
      }
  }

  $obj = new Test();
  echo $obj->publicVar; // Outputs: Public
  // echo $obj->privateVar; // Error: Cannot access private property
  // echo $obj->protectedVar; // Error: Cannot access protected property
  ```

## Advantages of OOP
- **Modularity**: Breaks complex problems into manageable classes, enhancing code organization and reusability.
- **Code Reusability**: Inheritance allows reusing code from parent classes, reducing redundancy.
- **Encapsulation**: Hides data, improving security and reducing unintended modifications.
- **DRY Principle**: "Don't Repeat Yourself" minimizes code duplication, easing maintenance and debugging.
- **Abstraction**: Simplifies problem-solving by focusing on essential features.
- **Polymorphism**: Enables flexible, reusable code through common interfaces or overridden methods.
- **Maintainability**: Modular structure simplifies updates and debugging.
- **Collaboration**: Well-defined class interfaces support teamwork and parallel development.

## Disadvantages of OOP
- **Steeper Learning Curve**: Concepts like inheritance and polymorphism can be challenging for beginners.
- **Overhead**: Objects consume more memory due to metadata and method tables; dynamic dispatch may slow execution.
- **Complexity**: Large systems with many objects can become hard to manage.
- **Inheritance Limitations**: Issues like the diamond problem or tight coupling can complicate code.
- **Parallel Programming Challenges**: Synchronizing objects in multi-threaded environments is complex.
- **Overuse of Abstraction**: Excessive abstraction can obscure implementation details, hindering debugging.
- **Performance Overhead**: Dynamic typing in PHP may slow execution compared to static typing.

## The `$this` Variable
- **Definition**: A special variable used within a class to refer to the current object, accessing its properties and methods.
- **Example**:
  ```php
  class NumberAdd {
      public function addNumbers($num1, $num2) {
          $sum = $num1 + $num2;
          echo "The sum of $num1 and $num2 is= $sum ";
      }
  }

  $addition = new NumberAdd();
  $addition->addNumbers(15, 10); // Outputs: The sum of 15 and 10 is= 25
  ```

## Practical Notes
- Use meaningful class and method names for clarity.
- Leverage encapsulation to protect data and expose only necessary interfaces.
- Use inheritance and interfaces to promote code reuse and flexibility.
- Avoid overcomplicating designs with excessive abstraction or deep inheritance hierarchies.
- Test classes thoroughly to ensure robust behavior across edge cases.