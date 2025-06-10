# Advanced Programming Concepts in C

## 4.1 Efficient Usage of Control Statements
- **Definition**: Control statements direct the flow of program execution based on logical conditions, enabling customized logic.
- **Purpose**: Determine the order of statement execution, allowing conditional and repetitive operations.
- **Types**:
  - Decision-making control statements
  - Conditional statements
  - Loop control statements
  - Branching statements

### 4.1.1 Decision-Making Control Statements
- **Simple `if` Statement**:
  - Executes a block of code if a condition is true; otherwise, skips to statements outside the block.
  - **Syntax**:
    ```c
    if (condition) {
        // Statements
    }
    ```
  - **Example**: Check if the first number is greater than the second.
    ```c
    #include <stdio.h>
    int main() {
        int a, b;
        printf("Enter two numbers: ");
        scanf("%d %d", &a, &b);
        if (a > b) {
            printf("%d is greater than %d\n", a, b);
        }
        return 0;
    }
    ```

- **If-Else Statement**:
  - Executes one block if the condition is true, another if false.
  - **Syntax**:
    ```c
    if (condition) {
        // True block
    } else {
        // False block
    }
    ```
  - **Example**:
    ```c
    #include <stdio.h>
    int main() {
        int num;
        printf("Enter a number: ");
        scanf("%d", &num);
        if (num % 2 == 0) {
            printf("%d is even\n", num);
        } else {
            printf("%d is odd\n", num);
        }
        return 0;
    }
    ```

- **Nested If-Else Statement**:
  - Contains additional `if` or `else` statements within an `if` or `else` block.
  - **Syntax**:
    ```c
    if (condition1) {
        if (condition2) {
            // Inner if block
        } else {
            // Inner else block
        }
    } else {
        if (condition3) {
            // Outer else's inner if block
        } else {
            // Outer else's else block
        }
    }
    ```
  - **Example**:
    ```c
    #include <stdio.h>
    int main() {
        int a, b, c;
        printf("Enter three numbers: ");
        scanf("%d %d %d", &a, &b, &c);
        if (a > b) {
            if (a > c) {
                printf("%d is largest\n", a);
            } else {
                printf("%d is largest\n", c);
            }
        } else {
            if (b > c) {
                printf("%d is largest\n", b);
            } else {
                printf("%d is largest\n", c);
            }
        }
        return 0;
    }
    ```

### 4.1.2 Conditional Control Statements
- **Switch Statement**:
  - Allows multi-way branching based on the value of an expression.
  - Transfers control to a matching `case` label or `default` if no match.
  - **Syntax**:
    ```c
    switch (expression) {
        case value1:
            // Statements
            break;
        case value2:
            // Statements
            break;
        default:
            // Statements
    }
    ```
  - **Example**:
    ```c
    #include <stdio.h>
    int main() {
        int choice;
        printf("Enter a number (1-3): ");
        scanf("%d", &choice);
        switch (choice) {
            case 1:
                printf("You chose One\n");
                break;
            case 2:
                printf("You chose Two\n");
                break;
            case 3:
                printf("You chose Three\n");
                break;
            default:
                printf("Invalid choice\n");
        }
        return 0;
    }
    ```

### 4.1.3 Loop Control Statements
- **While Loop**:
  - Entry-controlled; checks condition before executing the loop body.
  - **Syntax**:
    ```c
    while (condition) {
        // Statements
    }
    ```
  - **Example**:
    ```c
    #include <stdio.h>
    int main() {
        int i = 1;
        while (i <= 5) {
            printf("%d ", i);
            i++;
        }
        return 0;
    }
    ```

- **Do-While Loop**:
  - Exit-controlled; executes the loop body at least once before checking the condition.
  - **Syntax**:
    ```c
    do {
        // Statements
    } while (condition);
    ```
  - **Example**:
    ```c
    #include <stdio.h>
    int main() {
        int i = 1;
        do {
            printf("%d ", i);
            i++;
        } while (i <= 5);
        return 0;
    }
    ```

- **For Loop**:
  - Pre-test loop; includes initialization, condition, and update in one line.
  - **Syntax**:
    ```c
    for (initialization; condition; update) {
        // Statements
    }
    ```
  - **Example**:
    ```c
    #include <stdio.h>
    int main() {
        for (int i = 1; i <= 5; i++) {
            printf("%d ", i);
        }
        return 0;
    }
    ```

### 4.1.4 Branching Statements
- **Break**:
  - Terminates the nearest enclosing loop or switch statement.
  - **Example**:
    ```c
    #include <stdio.h>
    int main() {
        int counter = 0;
        while (counter < 8) {
            printf("%d ", counter);
            if (counter == 4)
                break;
            counter++;
        }
        return 0;
    }
    ```

- **Continue**:
  - Skips the current loop iteration and proceeds to the next.
  - **Example**:
    ```c
    #include <stdio.h>
    int main() {
        for (int counter = 0; counter < 8; counter++) {
            if (counter == 4)
                continue;
            printf("%d ", counter);
        }
        return 0;
    }
    ```

- **Return**:
  - Exits a function, optionally returning a value.
  - **Example**:
    ```c
    #include <stdio.h>
    int add(int a, int b) {
        return a + b;
    }
    int main() {
        printf("Sum: %d\n", add(3, 4));
        return 0;
    }
    ```

- **Goto**:
  - Jumps to a labeled statement; discouraged in structured programming.
  - **Example**:
    ```c
    #include <stdio.h>
    int main() {
        printf("Before goto\n");
        goto label;
        printf("This won't print\n");
        label:
        printf("After goto\n");
        return 0;
    }
    ```

- **Exit**:
  - Terminates the program, returning a status code to the operating system.
  - **Example**:
    ```c
    #include <stdio.h>
    #include <stdlib.h>
    int main() {
        FILE *fp = fopen("nonexistent.txt", "r");
        if (fp == NULL) {
            printf("File not found\n");
            exit(1);
        }
        fclose(fp);
        return 0;
    }
    ```

### Exercises
1. **Print Odd Numbers from 1 to N (While Loop)**:
   ```c
   #include <stdio.h>
   int main() {
       int n, i = 1;
       printf("Enter N: ");
       scanf("%d", &n);
       while (i <= n) {
           if (i % 2 != 0)
               printf("%d ", i);
           i++;
       }
       return 0;
   }
   ```

2. **Print Even Numbers from 1 to N (Do-While Loop)**:
   ```c
   #include <stdio.h>
   int main() {
       int n, i = 1;
       printf("Enter N: ");
       scanf("%d", &n);
       do {
           if (i % 2 == 0)
               printf("%d ", i);
           i++;
       } while (i <= n);
       return 0;
   }
   ```

3. **Print Uppercase Alphabets (While Loop)**:
   ```c
   #include <stdio.h>
   int main() {
       char ch = 'A';
       while (ch <= 'Z') {
           printf("%c ", ch);
           ch++;
       }
       return 0;
   }
   ```

4. **Print Multiplication Table (For Loop)**:
   ```c
   #include <stdio.h>
   int main() {
       int num;
       printf("Enter a number: ");
       scanf("%d", &num);
       for (int i = 1; i <= 10; i++) {
           printf("%d x %d = %d\n", num, i, num * i);
       }
       return 0;
   }
   ```

5. **Check Number Type (Zero, Positive, Negative)**:
   ```c
   #include <stdio.h>
   int main() {
       char input[10];
       while (1) {
           printf("Enter a number or 'e' to exit: ");
           scanf("%s", input);
           if (input[0] == 'e')
               break;
           int num = atoi(input);
           if (num == 0)
               printf("Zero\n");
           else if (num > 0)
               printf("Positive\n");
           else
               printf("Negative\n");
       }
       return 0;
   }
   ```

6. **Factorial Using Loop**:
   ```c
   #include <stdio.h>
   int main() {
       int n;
       long fact = 1;
       printf("Enter a number: ");
       scanf("%d", &n);
       for (int i = 1; i <= n; i++) {
           fact *= i;
       }
       printf("Factorial of %d = %ld\n", n, fact);
       return 0;
   }
   ```

7. **Sum of First N Natural Numbers**:
   ```c
   #include <stdio.h>
   int main() {
       int n, sum = 0;
       printf("Enter N: ");
       scanf("%d", &n);
       for (int i = 1; i <= n; i++) {
           sum += i;
       }
       printf("Sum = %d\n", sum);
       return 0;
   }
   ```

8. **Print Prime Numbers from 1 to N**:
   ```c
   #include <stdio.h>
   int main() {
       int n, i, j, isPrime;
       printf("Enter N: ");
       scanf("%d", &n);
       for (i = 2; i <= n; i++) {
           isPrime = 1;
           for (j = 2; j * j <= i; j++) {
               if (i % j == 0) {
                   isPrime = 0;
                   break;
               }
           }
           if (isPrime)
               printf("%d ", i);
       }
       return 0;
   }
   ```

### 4.1.5 Patterns Programming in C
- **Definition**: Art of generating visual patterns using symbols (e.g., stars, numbers) via nested loops.
- **Purpose**: Enhances understanding of loop control and logic.
- **Example: Pattern 2 (Right Triangle)**:
  ```c
  #include <stdio.h>
  int main() {
      for (int i = 0; i < 5; i++) {
          for (int j = 0; j <= i; j++) {
              printf("* ");
          }
          printf("\n");
      }
      return 0;
  }
  ```

- **Example: Pascal’s Triangle**:
  ```c
  #include <stdio.h>
  int main() {
      int height, r, c, pt[10][10];
      printf("Enter the height of triangle: ");
      scanf("%d", &height);
      for (r = 0; r < height; r++) {
          for (c = 0; c <= r; c++) {
              if (c == 0 || c == r)
                  pt[r][c] = 1;
              else
                  pt[r][c] = pt[r-1][c] + pt[r-1][c-1];
              printf("%d ", pt[r][c]);
          }
          printf("\n");
      }
      return 0;
  }
  ```

## 4.2 Efficient Usage of Functions and Pointers
### 4.2.1 Function Pointers
- **Definition**: Pointers that store the address of a function’s code in memory.
- **Syntax**:
  ```c
  return_type (*pointer_name)(parameter_types);
  ```
- **Example**:
  ```c
  #include <stdio.h>
  int add(int a, int b) { return a + b; }
  int main() {
      int (*fp)(int, int) = add;
      printf("Sum: %d\n", fp(3, 4));
      return 0;
  }
  ```

- **Using Function Pointers with Switch Replacement**:
  ```c
  #include <stdio.h>
  void add(int a, int b) { printf("Sum: %d\n", a + b); }
  void subtract(int a, int b) { printf("Difference: %d\n", a - b); }
  int main() {
      void (*ops[])(int, int) = {add, subtract};
      int choice, a, b;
      printf("Enter 0 for add, 1 for subtract: ");
      scanf("%d", &choice);
      printf("Enter two numbers: ");
      scanf("%d %d", &a, &b);
      if (choice >= 0 && choice < 2)
          ops[choice](a, b);
      else
          printf("Invalid choice\n");
      return 0;
  }
  ```

### 4.2.2 Function Returning a Pointer
- **Syntax**:
  ```c
  data_type *function_name(parameters) {
      // Code
  }
  ```
- **Note**: Avoid returning pointers to local variables, as they go out of scope.
- **Example**:
  ```c
  #include <stdio.h>
  #include <stdlib.h>
  int *create_array(int size) {
      int *arr = (int *)malloc(size * sizeof(int));
      for (int i = 0; i < size; i++)
          arr[i] = i + 1;
      return arr;
  }
  int main() {
      int *arr = create_array(5);
      for (int i = 0; i < 5; i++)
          printf("%d ", arr[i]);
      free(arr);
      return 0;
  }
  ```

### 4.2.3 Creating Custom Header Files
- **Purpose**: Store function declarations and data types for reuse across programs.
- **Example**:
  - **myHeadFile.h**:
    ```c
    #ifndef MYHEADFILE_H
    #define MYHEADFILE_H
    int add(int a, int b);
    int subtract(int a, int b);
    #endif
    ```
  - **main.c**:
    ```c
    #include <stdio.h>
    #include "myHeadFile.h"
    int add(int a, int b) { return a + b; }
    int subtract(int a, int b) { return a - b; }
    int main() {
        printf("Sum: %d\n", add(5, 3));
        printf("Difference: %d\n", subtract(5, 3));
        return 0;
    }
    ```

## 4.4.2 Linked Lists
- **Definition**: A data structure of nodes, each containing data and a pointer to the next node.
- **Node Structure**:
  ```c
  struct Node {
      int data;
      struct Node *next;
  };
  ```

### Types of Linked Lists
1. **Singly Linked List**:
   - Each node points to the next node.
   - **Example**:
     ```c
     #include <stdio.h>
     #include <stdlib.h>
     struct Node {
         int data;
         struct Node *next;
     };
     void insertAtBeginning(struct Node **head, int data) {
         struct Node *newNode = (struct Node *)malloc(sizeof(struct Node));
         newNode->data = data;
         newNode->next = *head;
         *head = newNode;
     }
     void printList(struct Node *head) {
         while (head != NULL) {
             printf("%d ", head->data);
             head = head->next;
         }
         printf("\n");
     }
     int main() {
         struct Node *head = NULL;
         insertAtBeginning(&head, 3);
         insertAtBeginning(&head, 2);
         insertAtBeginning(&head, 1);
         printList(head);
         return 0;
     }
     ```

2. **Doubly Linked List**:
   - Each node points to both the next and previous nodes.
   - **Example**:
     ```c
     #include <stdio.h>
     #include <stdlib.h>
     struct Node {
         int data;
         struct Node *prev;
         struct Node *next;
     };
     void insertAtBeginning(struct Node **head, int data) {
         struct Node *newNode = (struct Node *)malloc(sizeof(struct Node));
         newNode->data = data;
         newNode->prev = NULL;
         newNode->next = *head;
         if (*head != NULL)
             (*head)->prev = newNode;
         *head = newNode;
     }
     void printList(struct Node *head) {
         while (head != NULL) {
             printf("%d ", head->data);
             head = head->next;
         }
         printf("\n");
     }
     int main() {
         struct Node *head = NULL;
         insertAtBeginning(&head, 3);
         insertAtBeginning(&head, 2);
         insertAtBeginning(&head, 1);
         printList(head);
         return 0;
     }
     ```

3. **Circular Linked List**:
   - Last node points to the first node.
   - **Example**:
     ```c
     #include <stdio.h>
     #include <stdlib.h>
     struct Node {
         int data;
         struct Node *next;
     };
     void insert(struct Node **head, int data) {
         struct Node *newNode = (struct Node *)malloc(sizeof(struct Node));
         newNode->data = data;
         if (*head == NULL) {
             newNode->next = newNode;
             *head = newNode;
         } else {
             newNode->next = (*head)->next;
             (*head)->next = newNode;
         }
     }
     void display(struct Node *head) {
         if (head == NULL)
             return;
         struct Node *temp = head->next;
         do {
             printf("%d ", temp->data);
             temp = temp->next;
         } while (temp != head->next);
         printf("\n");
     }
     int main() {
         struct Node *head = NULL;
         insert(&head, 1);
         insert(&head, 2);
         insert(&head, 3);
         display(head);
         return 0;
     }
     ```

## 4.5 Proper Processing of File-Based C Programs
- **Purpose**: Store and retrieve data persistently using files, overcoming limitations of volatile memory.
- **Operations**:
  - Create, open, read, write, delete files.
- **Needs**:
  - **Reusability**: Access data anytime.
  - **Portability**: Transfer files without data loss.
  - **Efficiency**: Handle large data with minimal code.
  - **Storage Capacity**: Store extensive data.

### 4.5.1 Types of Files
1. **Text Files**:
   - Store ASCII characters; readable by text editors.
2. **Binary Files**:
   - Store data in binary format; more secure, program-readable.

### File Operations
- **Opening/Creating a File**:
  - **Syntax**:
    ```c
    FILE *f_ptr = fopen("filename", "mode");
    ```
  - **Modes**:
    - `r`: Read
    - `w`: Write (creates if not exists)
    - `a`: Append
    - `r+`, `w+`, `a+`: Read and write
  - **Example**:
    ```c
    FILE *f_ptr = fopen("abc.txt", "w");
    ```

- **Reading from a File**:
  - **Functions**:
    - `getc()`: Reads a character.
    - `getw()`: Reads an integer.
    - `fscanf()`: Reads formatted data.
    - `fgets()`: Reads a string.
    - `fread()`: Reads a block of data.
  - **Example: `fscanf`**:
    ```c
    #include <stdio.h>
    int main() {
        FILE *fp = fopen("data.txt", "r");
        int num;
        fscanf(fp, "%d", &num);
        printf("Read: %d\n", num);
        fclose(fp);
        return 0;
    }
    ```

- **Writing to a File**:
  - **Functions**: `putc()`, `putw()`, `fprintf()`, `fputs()`, `fwrite()`.
  - **Example: `fprintf`**:
    ```c
    #include <stdio.h>
    int main() {
        FILE *fp = fopen("output.txt", "w");
        fprintf(fp, "Hello, World!\n");
        fclose(fp);
        return 0;
    }
    ```

## Key Points
- Control statements (`if`, `switch`, loops, branching) manage program flow.
- Patterns use nested loops for visual output, enhancing loop mastery.
- Function pointers enable flexible function calls, reducing code redundancy.
- Custom header files promote modularity.
- Linked lists (singly, doubly, circular) offer dynamic data structures.
- File handling supports persistent data storage with text and binary files.