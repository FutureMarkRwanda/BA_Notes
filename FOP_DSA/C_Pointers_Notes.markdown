# Chapter 3: Pointers in C

## Overview of Pointers
- **Definition**: A pointer is a variable that stores the memory address of another variable, enabling indirect access and manipulation of data.
- **Purpose**: Enhances efficiency in handling arrays, structures, functions, and dynamic memory management.

## Address in C
- **Memory Address**: Every variable has a unique address in memory, accessible using the reference operator `&`.
  - Example: `&var` returns the address of variable `var`.
  - Commonly used in `scanf()` to store input at a variable’s address:
    ```c
    scanf("%d", &var);
    ```
- **Example Program**:
  ```c
  #include <stdio.h>
  int main() {
      int var = 5;
      printf("Value: %d\n", var);
      printf("Address: %lld\n", &var); // %lld for long long int address
      return 0;
  }
  ```
  **Sample Output**:
  ```
  Value: 5
  Address: 150408373932492
  ```
  - **Note**: Addresses vary by system and run-time. `%lld` is used for addresses in this example, though some compilers use `%p` for hexadecimal output or `%u` for unsigned integers.

## Creating Pointer Variables
- **Syntax**:
  ```c
  data_type *pointer_name;
  ```
  - Example: `int *p;` declares `p` as a pointer to an integer.
- **Note**: The `*` in declaration denotes a pointer, not the dereference operator.

### Reference (`&`) and Dereference (`*`) Operators
- **Reference Operator (`&`)**: Returns the memory address of a variable.
- **Dereference Operator (`*`)**: Accesses the value at the address stored in a pointer.
- **Example Program**:
  ```c
  #include <stdio.h>
  int main() {
      int *pc, c;
      c = 22;
      printf("Address of c: %lld\n", (long long)&c);
      printf("Value of c: %d\n\n", c);
      pc = &c; // pc stores address of c
      printf("Address stored in pc: %lld\n", (long long)pc);
      printf("Value pointed by pc: %d\n\n", *pc);
      c = 11; // Change c directly
      printf("Address stored in pc: %lld\n", (long long)pc);
      printf("Value pointed by pc: %d\n\n", *pc);
      *pc = 2; // Change value via pointer
      printf("Address of c: %lld\n", (long long)&c);
      printf("Value of c: %d\n\n", c);
      return 0;
  }
  ```
  **Explanation**:
  - `pc = &c;` assigns `c`’s address to `pc`.
  - `*pc` accesses/changes the value at that address.
  - Changing `c` affects `*pc` and vice versa, as they reference the same memory location.

## Call by Value vs. Call by Reference
- **Call by Value**:
  - Copies the value of actual parameters to formal parameters.
  - Changes to formal parameters do not affect actual parameters.
  - Separate memory is allocated for actual and formal parameters.
- **Call by Reference**:
  - Passes the address of actual parameters to formal parameters.
  - Changes to formal parameters affect actual parameters, as they point to the same memory.
- **Example 1: Increment Using Call by Reference**:
  ```c
  #include <stdio.h>
  void increment(int *var) {
      *var = *var + 1; // Modifies value at address
  }
  int main() {
      int num = 20;
      increment(&num); // Pass address
      printf("Value of num is: %d\n", num);
      return 0;
  }
  ```
  **Output**:
  ```
  Value of num is: 21
  ```

- **Example 2: Swapping Numbers Using Call by Reference**:
  ```c
  #include <stdio.h>
  void swapnum(int *var1, int *var2) {
      int tempnum = *var1;
      *var1 = *var2;
      *var2 = tempnum;
  }
  int main() {
      int num1 = 35, num2 = 45;
      printf("Before swapping:\nnum1 value is %d\nnum2 value is %d\n", num1, num2);
      swapnum(&num1, &num2);
      printf("After swapping:\nnum1 value is %d\nnum2 value is %d\n", num1, num2);
      return 0;
  }
  ```
  **Output**:
  ```
  Before swapping:
  num1 value is 35
  num2 value is 45
  After swapping:
  num1 value is 45
  num2 value is 35
  ```

## Pointer Access and Errors
- **Initialization**:
  - Pointers should be initialized to `NULL` or a valid address to avoid pointing to random memory.
  - Example:
    ```c
    int a = 5;
    int *ptr = NULL;
    ptr = &a; // Now points to a
    *ptr = 8; // Changes a to 8
    ```
  - Memory Representation (assuming 32-bit system):
    ```
    Address    Contents (Before ptr = &a)
    0x8130     0x00000005 (a = 5)
    0x8134     0x00000000 (ptr = NULL)

    Address    Contents (After ptr = &a)
    0x8130     0x00000005 (a = 5)
    0x8134     0x00008130 (ptr = &a)

    Address    Contents (After *ptr = 8)
    0x8130     0x00000008 (a = 8)
    0x8134     0x00008130 (ptr = &a)
    ```

- **Common Mistakes**:
  ```c
  int c, *pc;
  pc = c;      // Wrong: c is a value, not an address
  *pc = &c;    // Wrong: *pc is a value, &c is an address
  pc = &c;     // Correct: Assigns address to pointer
  *pc = c;     // Correct: Assigns value to pointed location
  ```
  - Uninitialized pointers or incorrect assignments can cause bugs or crashes.

## Strings and Pointers
- **String Decay**: String names act as pointers to the first character.
- **Example Program**:
  ```c
  #include <stdio.h>
  int main() {
      char name[] = "Harry Potter";
      printf("%c\n", *name);       // H
      printf("%c\n", *(name + 1)); // a
      printf("%c\n", *(name + 7)); // o
      char *namePtr = name;
      printf("%c\n", *namePtr);       // H
      printf("%c\n", *(namePtr + 1)); // a
      printf("%c\n", *(namePtr + 7)); // o
      return 0;
  }
  ```

## Dynamic Memory Allocation
- **Purpose**: Allows flexible memory allocation at runtime, unlike fixed-size arrays.
- **Functions** (from `<stdlib.h>`):
  - `malloc()`: Allocates uninitialized memory.
  - `calloc()`: Allocates initialized (zeroed) memory.
  - `free()`: Deallocates memory.
  - `realloc()`: Resizes allocated memory.

- **Syntax**:
  - `malloc`: `ptr = (castType*)malloc(size);`
    - Example: `ptr = (float*)malloc(100 * sizeof(float));` (400 bytes for 100 floats).
  - `calloc`: `ptr = (castType*)calloc(n, size);`
    - Example: `ptr = (float*)calloc(25, sizeof(float));` (100 bytes, initialized to 0).
  - `free`: `free(ptr);`
  - `realloc`: `ptr = realloc(ptr, new_size);`

- **Example 1: `malloc` and `free`**:
  ```c
  #include <stdio.h>
  #include <stdlib.h>
  int main() {
      int n, i, *ptr, sum = 0;
      printf("Enter number of elements: ");
      scanf("%d", &n);
      ptr = (int*)malloc(n * sizeof(int));
      if (ptr == NULL) {
          printf("Error! memory not allocated.\n");
          exit(0);
      }
      printf("Enter elements: ");
      for (i = 0; i < n; ++i) {
          scanf("%d", ptr + i);
          sum += *(ptr + i);
      }
      printf("Sum = %d\n", sum);
      free(ptr);
      return 0;
  }
  ```

- **Example 2: `calloc` and `free`**:
  ```c
  #include <stdio.h>
  #include <stdlib.h>
  int main() {
      int n, i, *ptr, sum = 0;
      printf("Enter number of elements: ");
      scanf("%d", &n);
      ptr = (int*)calloc(n, sizeof(int));
      if (ptr == NULL) {
          printf("Error! memory not allocated.\n");
          exit(0);
      }
      printf("Enter elements: ");
      for (i = 0; i < n; ++i) {
          scanf("%d", ptr + i);
          sum += *(ptr + i);
      }
      printf("Sum = %d\n", sum);
      free(ptr);
      return 0;
  }
  ```

- **Example 3: `realloc`**:
  ```c
  #include <stdio.h>
  #include <stdlib.h>
  int main() {
      int *ptr, i, n1, n2;
      printf("Enter size: ");
      scanf("%d", &n1);
      ptr = (int*)malloc(n1 * sizeof(int));
      printf("Addresses of previously allocated memory:\n");
      for (i = 0; i < n1; ++i)
          printf("%lld\n", (long long)(ptr + i));
      printf("Enter the new size: ");
      scanf("%d", &n2);
      ptr = realloc(ptr, n2 * sizeof(int));
      printf("Addresses of newly allocated memory:\n");
      for (i = 0; i < n2; ++i)
          printf("%lld\n", (long long)(ptr + i));
      free(ptr);
      return 0;
  }
  ```

## Benefits of Pointers
- **Efficiency**: Optimize handling of arrays and structures.
- **Function References**: Enable passing functions as arguments.
- **Reduced Code Length**: Simplify operations, reducing execution time.
- **Dynamic Memory Management**: Support flexible memory allocation.

## Key Points
- Pointers store memory addresses, accessed via `&` (reference) and `*` (dereference).
- Call by reference allows functions to modify actual parameters, unlike call by value.
- Strings decay to pointers, enabling direct manipulation.
- Dynamic memory allocation (`malloc`, `calloc`, `realloc`, `free`) supports runtime flexibility.
- Common pointer errors (e.g., uninitialized pointers) can cause undefined behavior.
- Pointers enhance efficiency and modularity in C programming.
- For further details, see: [Pointers Presentation](https://docs.google.com/presentation/d/1BamaqhnWuwhTwsuKhwEpDTAddLBuyuROBbe0jZRXg_w/edit#slide=id.g230e362be33_0_199).