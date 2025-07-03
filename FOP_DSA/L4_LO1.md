# **Learning Outcome 1: Apply C++ Programming Concepts**

### 📘 Learning Hours: 10

---

## 📌 Objective

By the end of this section, learners will be able to:
- Write and structure C++ programs using keywords and namespaces.
- Perform input/output operations effectively.
- Develop user-defined functions, including recursive ones.
- Apply Object-Oriented Programming (OOP) principles.
- Use templates for generic programming.


## 1. **C++ Program Basics**

### 1.1 Definition
A C++ program is a collection of functions, with `main()` as the entry point, using headers and namespaces to organize code.

### 1.2 Example: Basic Program
```cpp
#include <iostream>
using namespace std;
int main() {
    cout << "Hello, C++!" << endl;
    return 0;
}
```

### 1.3 Keywords
Reserved words that define C++ syntax (e.g., `int`, `class`, `return`).

| Keyword Examples        | Purpose                     |
|-------------------------|-----------------------------|
| `int`, `float`, `char`  | Data types                  |
| `if`, `else`, `switch`  | Control flow                |
| `for`, `while`, `do`    | Loops                       |
| `class`, `struct`       | Define user types           |

---

## 2. **Namespaces**

### 2.1 Definition
Namespaces group code to prevent naming conflicts.

### 2.2 Example: Namespace Usage
```cpp
namespace MySpace {
    int value = 100;
}
int main() {
    cout << MySpace::value << endl; // Access with scope resolution
    return 0;
}
```

### 2.3 Using Directive
```cpp
using namespace MySpace;
cout << value; // Direct access
```

---

## 3. **Input/Output Operations**

### 3.1 Definition
- **Input (`cin`)**: Reads data using `>>`.
- **Output (`cout`)**: Displays data using `<<`.

### 3.2 Example: I/O
```cpp
int num;
cout << "Enter a number: ";
cin >> num;
cout << "You entered: " << num << endl;
```

### 3.3 Complex Input
```cpp
string name;
getline(cin, name); // Read entire line
```

---

## 4. **User-Defined Functions**

### 4.1 Definition
Functions modularize code for reusability.

### 4.2 Example: Function
```cpp
int add(int a, int b) {
    return a + b;
}
int main() {
    cout << add(3, 4) << endl; // Outputs 7
}
```

### 4.3 Scope Rules
| Scope  | Description                     |
|--------|---------------------------------|
| Local  | Inside function/block           |
| Global | Outside all functions           |

---

## 5. **Recursive Functions**

### 5.1 Definition
A function that calls itself with a base case to terminate.

### 5.2 Example: Factorial
```cpp
int factorial(int n) {
    if (n <= 1) return 1; // Base case
    return n * factorial(n - 1); // Recursive call
}
```

---

## 6. **Object-Oriented Programming (OOP)**

### 6.1 Definition
OOP organizes code using classes and objects, supporting encapsulation, inheritance, and polymorphism.

### 6.2 Key Concepts
| Concept       | Description                         |
|---------------|-------------------------------------|
| Class         | Blueprint for objects               |
| Object        | Instance of a class                 |
| Encapsulation | Hiding data with access control     |
| Inheritance   | Reusing code via parent-child classes |
| Polymorphism  | Multiple forms of a function        |

### 6.3 Example: Class
```cpp
class Student {
public:
    string name;
    void display() {
        cout << "Name: " << name << endl;
    }
};
int main() {
    Student s;
    s.name = "Alice";
    s.display();
}
```

---

## 7. **Constructors and Destructors**

### 7.1 Definition
- **Constructor**: Initializes objects.
- **Destructor**: Cleans up resources.

### 7.2 Example
```cpp
class Box {
public:
    Box() { cout << "Constructor" << endl; }
    ~Box() { cout << "Destructor" << endl; }
};
```

---

## 8. **Polymorphism**

### 8.1 Definition
Allows functions to take multiple forms (overloading or overriding).

### 8.2 Example: Overriding
```cpp
class Animal {
public:
    virtual void sound() { cout << "Generic sound" << endl; }
};
class Dog : public Animal {
public:
    void sound() override { cout << "Woof!" << endl; }
};
```

---

## 9. **Templates**

### 9.1 Definition
Templates enable generic programming for reusable code.

### 9.2 Example: Function Template
```cpp
template <typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}
int main() {
    cout << max(5, 3) << endl; // Outputs 5
}
```

---

## ✅ Summary Table
| Concept       | Description                     | Example                         |
|---------------|---------------------------------|-------------------------------|
| Namespace     | Avoids naming conflicts         | `namespace MySpace`           |
| Function      | Modular code block              | `int add(int, int)`           |
| Recursion     | Self-calling function           | `factorial(n)`                |
| Class         | OOP blueprint                   | `class Student`               |
| Template      | Generic programming             | `template<typename T>`        |

---

## 📚 Practice Exercises
1. Write a C++ program to read two numbers and print their sum using a function.
2. Create a class `Rectangle` with attributes `length`, `width`, and methods to calculate area and perimeter.
3. Implement a recursive function to compute the sum of first `n` natural numbers.