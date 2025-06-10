# Chapter 3: Structures, Unions, and Enumerations in C

## Structures
- **Definition**: A structure is a user-defined data type that groups variables of different types under a single name, enabling efficient data organization.
- **Purpose**: Simplifies handling related data (e.g., storing a person’s name, citizenship number, and salary) compared to separate variables for each attribute.

### Defining a Structure
- **Syntax**:
  ```c
  struct [structure_name] {
      data_type member1;
      data_type member2;
      ...
      data_type memberN;
  } [variables];
  ```
- **Example**:
  ```c
  struct Person {
      char name[50];
      int citNo;
      float salary;
  };
  ```
  - Defines a `Person` structure with members `name`, `citNo`, and `salary`.

### Creating Structure Variables
- **Memory Allocation**: Defining a structure creates a type but allocates no memory until variables are declared.
- **Methods**:
  1. **Declare Variables with Definition**:
     ```c
     struct Person {
         char name[50];
         int citNo;
         float salary;
     } person0, person2, Peter, Moses, Nina, Rwema;
     ```
  2. **Declare Variables Separately**:
     ```c
     struct Person {
         char name[50];
         int citNo;
         float salary;
     };
     struct Person person1, person2, persons[20];
     ```
  - Both methods create variables `person1`, `person2`, and an array `persons[20]` of type `struct Person`.

### Accessing Structure Members
- **Operators**:
  - **Member Operator (`.`)**: Accesses members of a structure variable.
  - **Structure Pointer Operator (`->`)**: Accesses members via a pointer (discussed later).
- **Example**:
  ```c
  person2.salary = 50000.0; // Sets salary
  printf("Salary: %f\n", person2.salary); // Accesses salary
  ```

- **Example Program: Adding Distances**:
  ```c
  #include <stdio.h>
  struct Distance {
      int feet;
      float inch;
  } dist1, dist2, sum;
  int main() {
      printf("1st distance\n");
      printf("Enter feet: ");
      scanf("%d", &dist1.feet);
      printf("Enter inch: ");
      scanf("%f", &dist1.inch);
      printf("2nd distance\n");
      printf("Enter feet: ");
      scanf("%d", &dist2.feet);
      printf("Enter inch: ");
      scanf("%f", &dist2.inch);
      sum.feet = dist1.feet + dist2.feet;
      sum.inch = dist1.inch + dist2.inch;
      while (sum.inch >= 12) {
          ++sum.feet;
          sum.inch -= 12;
      }
      printf("Sum of distances = %d - %.1f\n", sum.feet, sum.inch);
      return 0;
  }
  ```

### Using `typedef` with Structures
- **Purpose**: Simplifies structure syntax by creating an alias for the structure type.
- **Syntax**:
  ```c
  typedef struct [structure_name] {
      data_type member1;
      data_type member2;
      ...
  } alias_name;
  ```
- **Example**:
  ```c
  typedef struct Distance {
      int feet;
      float inch;
  } distances;
  distances d1, d2; // Declare variables using alias
  ```
- **General `typedef` Usage**:
  ```c
  typedef existing_name alias_name;
  ```
  - Example: `typedef unsigned long ulong;` allows `ulong i, j;` for unsigned long variables.
- **Example Program with `typedef`**:
  ```c
  #include <stdio.h>
  #include <string.h>
  typedef struct {
      char name[50];
      int salary;
  } emp;
  int main() {
      emp e1;
      printf("Enter Employee record:\n");
      printf("Employee name: ");
      fgets(e1.name, sizeof(e1.name), stdin);
      printf("Enter Employee salary: ");
      scanf("%d", &e1.salary);
      printf("Employee name is %s", e1.name);
      printf("Salary is %d\n", e1.salary);
      return 0;
  }
  ```

### Accessing Structure Members Using Pointers
- **Operator**: `->` accesses members through a structure pointer.
- **Example Program**:
  ```c
  #include <stdio.h>
  struct person {
      int age;
      float weight;
  };
  int main() {
      struct person *personPtr, person1;
      personPtr = &person1;
      printf("Enter age: ");
      scanf("%d", &personPtr->age);
      printf("Enter weight: ");
      scanf("%f", &personPtr->weight);
      printf("Displaying:\n");
      printf("Age: %d\n", personPtr->age);
      printf("Weight: %f\n", personPtr->weight);
      return 0;
  }
  ```

### Dynamic Memory Allocation for Structures
- **Purpose**: Allocate memory for structures at runtime using `malloc` or `calloc`.
- **Example Program**:
  ```c
  #include <stdio.h>
  #include <stdlib.h>
  struct person {
      int age;
      float weight;
      char name[30];
  };
  int main() {
      struct person *ptr;
      int i, n;
      printf("Enter the number of persons: ");
      scanf("%d", &n);
      ptr = (struct person*)malloc(n * sizeof(struct person));
      for (i = 0; i < n; ++i) {
          printf("Enter first name and age respectively: ");
          scanf("%s %d", (ptr + i)->name, &(ptr + i)->age);
      }
      printf("Displaying Information:\n");
      for (i = 0; i < n; ++i) {
          printf("Name: %s\tAge: %d\n", (ptr + i)->name, (ptr + i)->age);
      }
      free(ptr);
      return 0;
  }
  ```

### Nested Structures
- **Definition**: Structures defined within another structure.
- **Example**:
  ```c
  struct complex {
      int imag;
      float real;
  };
  struct number {
      struct complex comp;
      int integers;
  } num1, num2;
  num2.comp.imag = 11; // Accessing nested member
  ```

### Size of Structures (Padding and Alignment)
- **Expectation**: Size of a structure is the sum of its members’ sizes.
- **Reality**: Compilers add padding for alignment, increasing size.
- **Example 1: Structure A**:
  ```c
  struct A {
      int a;      // 4 bytes
      int* b;     // 8 bytes
      char c;     // 1 byte
      char* d;    // 8 bytes
  };
  ```
  - Expected size: `4 + 8 + 1 + 8 = 21` bytes.
  - Actual size (64-bit system): 32 bytes due to padding.
  - **Alignment**: Members are aligned to the largest member size (8 bytes for pointers).
  ```c
  #include <stdio.h>
  int main() {
      struct A a;
      printf("Size of struct A: %lu\n", sizeof(struct A));
      return 0;
  }
  ```
  **Output**: `Size of struct A: 32`

- **Example 2: Structure B (Reordered)**:
  ```c
  struct B {
      int* b;     // 8 bytes
      char c;     // 1 byte
      int a;      // 4 bytes
      char* d;    // 8 bytes
  };
  ```
  - Actual size: 24 bytes due to optimized alignment.
  ```c
  #include <stdio.h>
  int main() {
      struct B b;
      printf("Size of struct B: %lu\n", sizeof(struct B));
      return 0;
  }
  ```
  **Output**: `Size of struct B: 24`
  - **Note**: Compilers cannot reorder members, but member order affects padding.

## Unions
- **Definition**: A user-defined type similar to structures, but all members share a single memory location equal to the size of the largest member.
- **Purpose**: Conserves memory when only one member is used at a time.
- **Syntax**:
  ```c
  union [union_name] {
      data_type member1;
      data_type member2;
      ...
  } [variables];
  ```

### Accessing Union Members
- **Syntax**: Same as structures, using the `.` operator.
- **Example Program**:
  ```c
  #include <stdio.h>
  union item {
      int a;
      char ch;
  };
  int main() {
      union item it;
      it.a = 12;
      printf("a: %d\n", it.a);
      it.ch = 'z';
      printf("ch: %c\n", it.ch);
      printf("a: %d\n", it.a); // May show corrupted value
      printf("ch: %c\n", it.ch);
      return 0;
  }
  ```
  - **Note**: Assigning to one member overwrites others, as they share the same memory.

## Enumerations
- **Definition**: A user-defined type that assigns names to integral constants, improving code readability and maintainability.
- **Syntax**:
  ```c
  enum enum_name { const1, const2, ... };
  enum enum_name variable;
  ```
- **Example Program**:
  ```c
  #include <stdio.h>
  enum week { Mon=10, Tue, Wed, Thur, Fri=10, Sat=16, Sun };
  enum day { Mond, Tues, Wedn, Thurs, Frid=18, Satu=11, Sund };
  int main() {
      printf("The value of enum week: %d\t%d\t%d\t%d\t%d\t%d\t%d\n",
             Mon, Tue, Wed, Thur, Fri, Sat, Sun);
      printf("The default value of enum day: %d\t%d\t%d\t%d\t%d\t%d\t%d\n",
             Mond, Tues, Wedn, Thurs, Frid, Satu, Sund);
      return 0;
  }
  ```
  - **Behavior**: If not explicitly assigned, constants increment from 0 or the previous value.

## Key Points
- **Structures**: Group different data types under one name, accessed via `.` or `->` (for pointers).
- **Typedef**: Simplifies structure declarations with aliases.
- **Dynamic Allocation**: Use `malloc` for runtime structure allocation.
- **Nested Structures**: Allow structures within structures for complex data.
- **Padding**: Compilers align structure members, affecting size; order matters.
- **Unions**: Share memory among members, saving space but allowing only one active member.
- **Enumerations**: Assign names to integer constants for readability.