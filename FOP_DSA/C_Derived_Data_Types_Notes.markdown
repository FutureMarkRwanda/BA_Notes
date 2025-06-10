# Chapter 3: C Derived Data Types

## Overview of Derived Data Types
- **Definition**: Derived data types are constructed from primary data types (e.g., `int`, `char`, `float`) by grouping or modifying them. Examples include arrays, structures, unions, pointers, and functions.
- **Purpose**: Allow complex data organization and manipulation.
- **Variable Declaration**: Every variable must be declared with a specific data type, determining the type of data it can hold throughout its lifetime (e.g., `int x` can only hold integer values).

## Arrays
- **Definition**: A collection of a fixed number of elements of the same data type stored in contiguous memory locations.
- **Key Characteristics**:
  - Fixed size, cannot be changed after declaration.
  - Elements are accessed via indices, starting at 0.
  - No built-in bounds checking in C, which can lead to errors if indices are out of range.

### One-Dimensional Arrays
- **Declaration**:
  ```c
  type name[number_of_elements];
  ```
  Examples:
  ```c
  int numbers[6]; // Array of 6 integers
  char letters[6]; // Array of 6 characters
  ```

- **Initialization**:
  - Initialize during declaration with comma-separated values in curly braces:
    ```c
    int point[6] = {0, 0, 1, 0, 0, 0};
    ```
  - Size can be omitted if initialized, as the compiler infers it:
    ```c
    int point[] = {0, 0, 1, 0, 0, 0}; // Automatically sized to 6
    ```
  - Partial initialization sets remaining elements to default values (e.g., 0 for integers):
    ```c
    int numbers[2000] = {25}; // First element is 25, others are 0
    ```

- **Accessing Elements**:
  - Use indices starting at 0:
    ```c
    int x = point[2]; // x = 3 (index 2 holds 3)
    ```
  - Out-of-bounds access (e.g., `point[15]`, `point[-4]`) may not raise errors but can cause undefined behavior.

- **Array Size Calculation**:
  - Use `sizeof()` to determine the number of elements:
    ```c
    short anArray[] = {3, 567, 9, 12, 15};
    int size = sizeof(anArray) / sizeof(short); // size = 5
    ```
  - Common in loops to avoid hardcoding array size:
    ```c
    for (int ix = 0; ix < (sizeof(anArray) / sizeof(short)); ++ix) {
        // Process anArray[ix]
    }
    ```

- **Key Notes**:
  - First index is 0, not 1.
  - Last element index is `n-1` for an array of size `n`.
  - Memory addresses are contiguous, incrementing by the size of the data type (e.g., `float` increments by 4 bytes).

### Two-Dimensional Arrays
- **Definition**: Arrays of arrays, forming a rectangular grid of rows and columns.
- **Declaration**:
  ```c
  type name[rows][columns];
  ```
  Example:
  ```c
  char two_d[3][5]; // 3 rows, 5 columns
  ```

- **Initialization**:
  - Initialize with nested curly braces or a single list:
    ```c
    int two_d[2][3] = {{5, 2, 1}, {6, 7, 8}}; // 2 rows, 3 columns
    int two_d[][3] = {{1, 3, 0}, {-1, 5, 9}}; // Rows inferred
    int two_d[2][3] = {1, 3, 0, -1, 5, 9}; // Linear initialization
    ```

- **Accessing/Modifying**:
  ```c
  char ch = two_d[2][4]; // Access element at row 2, column 4
  two_d[0][0] = 'x'; // Set element at row 0, column 0
  ```

- **Three-Dimensional Arrays**:
  ```c
  float y[2][4][3]; // Holds 24 elements (2 * 4 * 3)
  int test[2][3][4] = {{{3, 4, 2, 3}, {0, -3, 9, 11}, {23, 12, 23, 2}},
                       {{13, 4, 56, 3}, {5, 9, 3, 5}, {3, 1, 4, 9}}};
  ```

### Strings (Character Arrays)
- **Definition**: Arrays of `char` terminated by a null character (`'\0'`).
- **Declaration**:
  ```c
  char s[5]; // Array for 4 characters + null terminator
  ```

- **Initialization**:
  ```c
  char c[] = "abcd"; // Compiler adds '\0'
  char c[50] = "abcd"; // Remaining elements are 0
  char c[] = {'a', 'b', 'c', 'd', '\0'}; // Explicit null terminator
  char c[5] = {'a', 'b', 'c', 'd', '\0'};
  ```

- **Reading Strings**:
  - `scanf()` reads until whitespace:
    ```c
    #include <stdio.h>
    int main() {
        char name[20];
        printf("Enter name: ");
        scanf("%s", name); // Stops at whitespace
        printf("Your name is %s.\n", name);
        return 0;
    }
    ```
    **Output Issue**: If input is "Dennis Ritchie", only "Dennis" is stored due to whitespace.

  - `gets()` (deprecated) or `fgets()` reads a full line:
    ```c
    #include <stdio.h>
    int main() {
        char name[30];
        printf("Enter name: ");
        fgets(name, sizeof(name), stdin); // Reads entire line
        printf("Your Name is: ");
        puts(name); // Displays string
        return 0;
    }
    ```

- **String Handling Functions** (from `<string.h>`):
  | **Function** | **Description**                     |
  |--------------|-------------------------------------|
  | `strlen()`   | Computes string length (excludes `\0`) |
  | `strcpy()`   | Copies one string to another        |
  | `strcat()`   | Concatenates two strings            |
  | `strcmp()`   | Compares two strings                |
  | `strlwr()`   | Converts string to lowercase        |
  | `strupr()`   | Converts string to uppercase        |

- **Passing Strings to Functions**:
  ```c
  #include <stdio.h>
  #include <string.h>
  void displayString(char str[]);
  int main() {
      char str[50];
      printf("Enter string: ");
      fgets(str, sizeof(str), stdin);
      displayString(str);
      return 0;
  }
  void displayString(char str[]) {
      printf("The passed String was: ");
      puts(str);
  }
  ```

- **Key Notes**:
  - Strings are null-terminated character arrays.
  - Compiler automatically adds `'\0'` for string literals.
  - Long strings can be split across lines:
    ```c
    char string[58] = "This is a very, very long " "string that requires two lines.";
    ```
  - Avoid deprecated methods like backslash line continuation.
  - Use `<string.h>` for string manipulation functions.

## Array Sorting Algorithms
Sorting involves rearranging elements in a specific order (e.g., ascending or descending) by swapping elements.

### Bubble Sort
- **Definition**: Compares adjacent elements and swaps them if they are in the wrong order, "bubbling" the largest element to the end each iteration.
- **Process** (for ascending order):
  1. Compare adjacent elements.
  2. Swap if the first is greater than the second.
  3. Repeat for `n-1` iterations for an array of size `n`.
- **Example Array**: `{5, 1, 6, 2, 4, 3}`
  - After first iteration: `{1, 5, 2, 4, 3, 6}` (6 bubbles to the end).
  - Continues until sorted.

### Selection Sort
- **Definition**: Repeatedly selects the smallest (or largest) element from the unsorted portion and swaps it with the first unsorted element.
- **Process** (for ascending order):
  1. Find the smallest element in the array and swap it with the first element.
  2. Move to the next position and find the smallest element in the remaining subarray.
  3. Repeat until sorted.
- **Example Array**: `{3, 6, 1, 8, 4, 5}`
  - First pass: Swap 1 with 3 → `{1, 6, 3, 8, 4, 5}`.
  - Second pass: Swap 3 with 6 → `{1, 3, 6, 8, 4, 5}`.
  - Continues until sorted.
- **Implementation**:
  ```c
  #include <stdio.h>
  void swap(int array[], int firstIndex, int secondIndex) {
      int temp = array[firstIndex];
      array[firstIndex] = array[secondIndex];
      array[secondIndex] = temp;
  }
  int indexOfMinimum(int array[], int startIndex, int n) {
      int minValue = array[startIndex];
      int minIndex = startIndex;
      for (int i = minIndex + 1; i < n; i++) {
          if (array[i] < minValue) {
              minIndex = i;
              minValue = array[i];
          }
      }
      return minIndex;
  }
  void selectionSort(int array[], int n) {
      for (int i = 0; i < n; i++) {
          int index = indexOfMinimum(array, i, n);
          swap(array, i, index);
      }
  }
  void printArray(int array[], int size) {
      for (int i = 0; i < size; i++) {
          printf("%d ", array[i]);
      }
      printf("\n");
  }
  int main() {
      int array[] = {46, 52, 21, 22, 11};
      int n = sizeof(array) / sizeof(array[0]);
      selectionSort(array, n);
      printf("Sorted array: \n");
      printArray(array, n);
      return 0;
  }
  ```
- **Note**: Selection sort is unstable (may change order of equal elements) but can be stable with linked lists.

### Insertion Sort
- **Definition**: Builds a sorted array by inserting each element into its correct position in the sorted portion.
- **Characteristics**:
  - Efficient for small or partially sorted datasets.
  - Adaptive: Fewer steps for partially sorted arrays.
  - Stable: Preserves relative order of equal elements.
  - Space-efficient: Requires only one extra memory space.
- **Process** (for ascending order):
  1. Start with the second element (index 1) as the key.
  2. Compare the key with elements to its left and insert it in the correct position.
  3. Repeat for each subsequent element.
- **Example Array**: `{4, 3, 2, 10, 12, 1, 5, 6}`
  - First pass: Key = 3, insert before 4 → `{3, 4, 2, 10, 12, 1, 5, 6}`.
  - Second pass: Key = 2, insert before 3 → `{2, 3, 4, 10, 12, 1, 5, 6}`.
  - Continues until sorted.
- **Implementation**:
  ```c
  #include <stdio.h>
  void insertionSort(int array[], int length) {
      int i, j, key;
      for (i = 1; i < length; i++) {
          j = i;
          while (j > 0 && array[j - 1] > array[j]) {
              key = array[j];
              array[j] = array[j - 1];
              array[j - 1] = key;
              j--;
          }
      }
      printf("Sorted Array: ");
      printArray(array, length);
  }
  void printArray(int array[], int size) {
      for (int j = 0; j < size; j++) {
          printf(" %d ", array[j]);
      }
      printf("\n");
  }
  int main() {
      int array[] = {4, 3, 2, 10, 12, 1, 5, 6};
      insertionSort(array, 8);
      return 0;
  }
  ```

## Key Points
- Derived data types like arrays extend primary types for complex data management.
- Arrays store fixed-size collections of the same type, with zero-based indexing.
- Strings are character arrays with a null terminator (`'\0'`), supported by `<string.h>` functions.
- Sorting algorithms (Bubble, Selection, Insertion) rearrange arrays by swapping elements:
  - **Bubble Sort**: Compares and swaps adjacent elements, inefficient for large datasets.
  - **Selection Sort**: Selects the smallest element for each position, simple but unstable.
  - **Insertion Sort**: Inserts elements into a sorted subarray, efficient for small or partially sorted data.
- Use `sizeof()` to safely handle array sizes in loops.
- Avoid out-of-bounds access to prevent undefined behavior.
- For exercises on arrays, refer to: [Array Exercises](https://docs.google.com/document/d/1VqPHsUimzYNoiUkshNFjDOoeQb7_sJSv/edit).