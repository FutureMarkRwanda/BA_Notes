# Unit 6: Pointers and Structures in C++

## 6.1 Pointers in C++
Pointers are variables that store memory addresses, allowing direct manipulation of memory in C++.

- **Definition**: A pointer is a variable that holds the memory address of another variable.
- **Syntax**:
  - Declare a pointer: `type* pointer_name;`
  - `*`: Dereference operator to access the value at the address.
  - `&`: Address-of operator to get a variable’s address.
- **Key Concepts**:
  - Pointers allow efficient memory access and manipulation.
  - Must be initialized to avoid undefined behavior.
  - Null pointer: `pointer_name = nullptr;` (safe initialization).
- **Example**:
  ```cpp
  #include <iostream>
  int main() {
      int x = 10;
      int* ptr = &x; // Pointer stores address of x
      std::cout << "Value of x: " << x << std::endl; // Output: 10
      std::cout << "Address of x: " << ptr << std::endl; // Output: Address
      std::cout << "Value at ptr: " << *ptr << std::endl; // Output: 10
      *ptr = 20; // Change value at address
      std::cout << "New value of x: " << x << std::endl; // Output: 20
      return 0;
  }
  ```
- **Uses**: Dynamic memory allocation, passing parameters by reference, arrays, and data structures.

## 6.2 Memory Allocation
Memory allocation in C++ involves managing memory for variables and data structures during program execution.

- **Types of Memory**:
  - **Stack**: Automatic memory for local variables (e.g., function variables).
    - Fast, but limited size and lifetime (scope-based).
  - **Heap**: Dynamic memory allocated manually, persists until deallocated.
    - Larger, but requires explicit management.
- **Dynamic Memory Allocation**:
  - **new**: Allocates memory on the heap.
  - **delete**: Frees allocated memory to prevent memory leaks.
  - Syntax: `type* ptr = new type;` and `delete ptr;`.
- **Example (Dynamic Allocation)**:
  ```cpp
  #include <iostream>
  int main() {
      int* ptr = new int; // Allocate memory for an integer
      *ptr = 42; // Store value
      std::cout << "Value: " << *ptr << std::endl; // Output: 42
      delete ptr; // Free memory
      ptr = nullptr; // Avoid dangling pointer
      return 0;
  }
  ```
- **Array Allocation**:
  - Allocate: `type* ptr = new type[size];`
  - Deallocate: `delete[] ptr;`
- **Example (Dynamic Array)**:
  ```cpp
  #include <iostream>
  int main() {
      int size = 3;
      int* arr = new int[size]; // Allocate array
      arr[0] = 1; arr[1] = 2; arr[2] = 3;
      for (int i = 0; i < size; i++) {
          std::cout << arr[i] << " "; // Output: 1 2 3
      }
      delete[] arr; // Free array memory
      return 0;
  }
  ```
- **Memory Management Tips**:
  - Always free allocated memory to avoid leaks.
  - Set pointers to `nullptr` after deletion to prevent dangling pointers.
  - Avoid accessing memory after deallocation.

## 6.3 C++ Structures
Structures in C++ group related data of different types into a single unit.

- **Definition**: A `struct` is a user-defined data type that combines multiple variables (members) of different types.
- **Syntax**:
  ```cpp
  struct StructureName {
      type member1;
      type member2;
      // ...
  };
  ```
- **Accessing Members**: Use the dot operator (`.`) for objects or arrow operator (`->`) for pointers to structures.
- **Example**:
  ```cpp
  #include <iostream>
  #include <string>
  struct Student {
      int id;
      std::string name;
      float gpa;
  };
  int main() {
      // Create a structure variable
      Student s1;
      s1.id = 1;
      s1.name = "Alice";
      s1.gpa = 3.8;
      std::cout << "ID: " << s1.id << ", Name: " << s1.name << ", GPA: " << s1.gpa << std::endl;
      // Using a pointer to structure
      Student* ptr = &s1;
      std::cout << "ID via pointer: " << ptr->id << std::endl; // Output: 1
      return 0;
  }
  ```
- **Uses**:
  - Organize related data (e.g., student records).
  - Pass multiple data items as a single parameter.
  - Foundation for complex data structures like linked lists.
- **Example with Pointers**:
  ```cpp
  #include <iostream>
  #include <string>
  struct Student {
      int id;
      std::string name;
      float gpa;
  };
  int main() {
      Student* s2 = new Student; // Dynamic allocation
      s2->id = 2;
      s2->name = "Bob";
      s2->gpa = 3.5;
      std::cout << "ID: " << s2->id << ", Name: " << s2->name << ", GPA: " << s2->gpa << std::endl;
      delete s2; // Free memory
      return 0;
  }
  ```