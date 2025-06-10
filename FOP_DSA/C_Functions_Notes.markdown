# Chapter 3: Functions in C

## Overview of Functions
- **Definition**: A function is a block of code enclosed in `{}` that performs a specific task, providing reusability and modularity.
- **Purpose**: Breaks down large programs into manageable, reusable units called procedures or subroutines in other languages.

### Advantages of Functions
- **Code Reuse**: Avoid rewriting the same logic by calling functions multiple times.
- **Modularity**: Divide large programs into smaller, trackable units.
- **Maintainability**: Simplifies debugging and updates.
- **Reusability**: Functions can be called from any part of the program.

## Function Aspects
Functions in C have three key aspects:

| **Aspect**           | **Description**                                                                 | **Syntax**                                    |
|----------------------|--------------------------------------------------------------------------------|-----------------------------------------------|
| **Declaration**      | Declares function name, parameters, and return type globally (optional for some compilers). | `return_type function_name(parameters_list);` |
| **Call**            | Invokes the function with arguments matching the declaration.                    | `function_name(argument_list);`               |
| **Definition**       | Contains the actual code (function body) executed when called.                  | `return_type function_name(parameters_list) { body; }` |

- **Note**: In declarations, parameter names can be omitted, specifying only types (e.g., `void myFunction(int, char, float);`).
- Function declaration is not mandatory for some C compilers.

## Types of Functions
1. **Library Functions**:
   - Predefined in C header files (e.g., `scanf()`, `printf()`, `gets()`, `puts()`, `ceil()`, `floor()`, `sin()`, `cos()`).
   - Require including the relevant header file (e.g., `<stdio.h>`, `<math.h>`).
2. **User-Defined Functions**:
   - Created by programmers to simplify and optimize code.
   - Examples include custom functions for specific tasks.

## Function Call Variations
Functions vary based on whether they accept arguments or return values:

1. **No Arguments, No Return Value**:
   ```c
   #include <stdio.h>
   void display() {
       char names[50];
       printf("Enter your names: \n");
       fgets(names, sizeof(names), stdin);
       printf("You said your names are: \n");
       puts(names);
   }
   int main() {
       display();
       return 0;
   }
   ```

2. **With Arguments, No Return Value**:
   ```c
   #include <stdio.h>
   void add(int a, int b) {
       printf("The sum of %d and %d is %d \n", a, b, a + b);
   }
   int main() {
       int n1, n2;
       printf("Enter two integers \n");
       scanf("%d%d", &n1, &n2);
       add(n1, n2);
       return 0;
   }
   ```

3. **With Arguments, With Return Value**:
   ```c
   #include <stdio.h>
   int sum(int a, int b) {
       return a + b;
   }
   int main() {
       int n1, n2, s;
       printf("Enter two integers \n");
       scanf("%d%d", &n1, &n2);
       s = sum(n1, n2);
       printf("The calculated sum is %d \n", s);
       return 0;
   }
   ```

4. **No Arguments, With Return Value**:
   ```c
   #include <stdio.h>
   float square() {
       float side;
       printf("Give the side of Square\n");
       scanf("%f", &side);
       return side * side;
   }
   int main() {
       float area = square();
       printf("The area of the square is %f \n", area);
       return 0;
   }
   ```

## Recursive Functions
- **Definition**: A function that calls itself, either directly or indirectly, to solve smaller instances of a problem until a base condition is met.
- **Key Components**:
  - **Base Case**: Condition to stop recursion, preventing infinite loops.
  - **Recursive Case**: The function calls itself with modified parameters.
- **Pseudocode Structure**:
  ```c
  if (base_condition) {
      return given_value;
  } else if (another_base_condition) {
      return other_value;
  } else {
      // Statement
      recursive_call;
  }
  ```

### Examples
1. **Fibonacci Series (nth Element)**:
   ```c
   #include <stdio.h>
   int numberfibonacci(int a) {
       if (a == 0) {
           return 0;
       } else if (a == 1) {
           return 1;
       } else {
           return numberfibonacci(a - 1) + numberfibonacci(a - 2);
       }
   }
   int main() {
       int a, b;
       printf("Please enter the value of the n number here (index in Fibonacci series): ");
       scanf("%d", &a);
       b = numberfibonacci(a);
       printf("The element at index %d in Fibonacci series is %d \n", a, b);
       return 0;
   }
   ```

2. **Factorial Using Recursion**:
   ```c
   #include <stdio.h>
   long factorial(int n) {
       if (n == 0 || n == 1) {
           return 1;
       } else {
           return n * factorial(n - 1);
       }
   }
   int main() {
       int number;
       printf("Enter a Positive number: ");
       scanf("%d", &number);
       printf("The Factorial of %d is %ld \n", number, factorial(number));
       return 0;
   }
   ```

### Recursion: Advantages and Disadvantages
- **Advantages**:
  - Elegant and readable code.
  - Simplifies complex problems (e.g., Fibonacci, factorial).
- **Disadvantages**:
  - Slower than loops due to multiple function calls.
  - Risk of stack overflow for deep recursion.
  - Every recursive function can be rewritten as a loop for better performance, though code may be less readable.
- **Choice**: Use recursion for clarity when performance is not critical; use loops for efficiency.

## Exercises
1. **Rectangle Area Function**:
   - Write a function `rectangleArea` that takes two sides (`side1`, `side2`) as arguments and returns the area.
   ```c
   #include <stdio.h>
   float rectangleArea(float side1, float side2) {
       return side1 * side2;
   }
   int main() {
       float s1, s2;
       printf("Enter two sides of the rectangle: ");
       scanf("%f %f", &s1, &s2);
       printf("Area of rectangle: %f\n", rectangleArea(s1, s2));
       return 0;
   }
   ```

2. **Sum of Series (1 + 1/2! + 1/3! + ... + 1/n!)**:
   - Write a program to compute the sum of the series using a user-defined function, where `n` is provided at runtime.
   ```c
   #include <stdio.h>
   long factorial(int n) {
       if (n == 0 || n == 1) return 1;
       return n * factorial(n - 1);
   }
   double seriesSum(int n) {
       double sum = 0.0;
       for (int i = 1; i <= n; i++) {
           sum += 1.0 / factorial(i);
       }
       return sum;
   }
   int main() {
       int n;
       printf("Enter n for the series sum (1 + 1/2! + ... + 1/n!): ");
       scanf("%d", &n);
       printf("Sum of series: %lf\n", seriesSum(n));
       return 0;
   }
   ```

3. **Swap Two Numbers**:
   - Write a function to swap two numbers.
   ```c
   #include <stdio.h>
   void swap(int *a, int *b) {
       int temp = *a;
       *a = *b;
       *b = temp;
   }
   int main() {
       int x, y;
       printf("Enter two numbers: ");
       scanf("%d %d", &x, &y);
       printf("Before swap: x = %d, y = %d\n", x, y);
       swap(&x, &y);
       printf("After swap: x = %d, y = %d\n", x, y);
       return 0;
   }
   ```

## Key Points
- Functions divide programs into reusable, modular blocks.
- Three aspects: declaration (optional for some compilers), call, and definition.
- Two types: library (predefined) and user-defined (custom).
- Functions vary by arguments and return values, enabling flexibility.
- Recursive functions call themselves, requiring a base case to avoid infinite loops.
- Recursion is elegant but slower; loops are faster but may be less readable.
- Exercises like `rectangleArea`, series sum, and swapping demonstrate practical function use.