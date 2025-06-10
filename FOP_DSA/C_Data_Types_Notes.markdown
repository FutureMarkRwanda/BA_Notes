# Chapter 3: C Data Types

## Prerequisites
- **Number Systems**: Understand binary, decimal, and other number systems. Refer to: [Number Systems Document](https://docs.google.com/document/d/1OtiVijwX7A96kC1ifrE3KHj1U-UgpvhN/edit?usp=sharing&ouid=111492439619719304666&rtpof=true&sd=true)

## Categories of Data Types in C
C language categorizes data types into five groups:

| **Category**     | **Examples**                              |
|-------------------|-------------------------------------------|
| **Primary**       | Character, Integer, Floating-point, Double |
| **Derived**       | Array, Structure, Union, Pointer, Function |
| **Enumeration**   | Enums                                     |
| **Bool Type**     | `true` or `false`                         |
| **Void**          | Empty value                               |

## Primary Data Types
C has five primary (primitive) data types:

1. **Character (`char`)**: Stores single ASCII characters (e.g., `'a'`, `'B'`).
2. **Integer (`int`)**: Stores whole numbers (e.g., 1, 1000).
3. **Floating-point (`float`)**: Stores decimal or real numbers (e.g., 99.9, 10.5).
4. **Double (`double`)**: Stores large numeric values with higher precision than `float`.
5. **Void (`void`)**: Represents no value, often used in functions.

### Keywords for Primary Data Types
| **Data Type**     | **Keyword** |
|-------------------|-------------|
| Character         | `char`      |
| Integer           | `int`       |
| Floating-point    | `float`     |
| Double            | `double`    |
| Void              | `void`      |

## Size of Data Types
The size of data types varies based on the compiler and processor architecture (1 byte = 8 bits).

### Character (`char`)
- **Size**: 1 byte (8 bits).
- Consistent across most compilers and processors.

### Integer (`int`)
- **Size**: Matches the word length of the execution environment:
  - 16-bit environment: 2 bytes (16 bits).
  - 32-bit environment: 4 bytes (32 bits).
  - 64-bit environment: Typically 4 bytes (32 bits), not 8 bytes.

### Floating-point (`float`)
- **Size**: 4 bytes (32 bits).
- Single-precision, used for decimal values.
- Faster than `double` due to smaller size.

### Double (`double`)
- **Size**: 8 bytes (64 bits).
- Double-precision, stores larger values than `float`.
- Structure: 1 bit (sign), 11 bits (exponent), 52 bits (mantissa).
- Precision: ~15–17 digits (before and after decimal).

### Void (`void`)
- **Size**: 0 bytes (no value).

## Data Type Modifiers
Modifiers refine primary data types for specific use cases:
- **Signed**: Supports positive and negative values.
- **Unsigned**: Supports only positive values.
- **Long**: Increases the range of values.
- **Short**: Decreases the range of values.

**Examples**:
- `signed int`, `unsigned int`, `short int`, `long int`.

**Default Behavior**:
- If a modifier is used without a data type, `int` is assumed (e.g., `unsigned` = `unsigned int`, `long` = `long int`).

### Signed vs. Unsigned
- **Signed**: Uses the most significant bit (MSB) as a sign flag (0 = positive, 1 = negative).
  - Example: For a 16-bit `signed int`, `11111111 11111111` = -32,767.
- **Unsigned**: Uses all bits for the number, increasing the positive range.
  - Example: For a 16-bit `unsigned int`, `11111111 11111111` = 65,535.
- **Impact**: Signed types use one bit for the sign, reducing the range of representable numbers.

## Data Type Value Ranges
The table below shows typical sizes, ranges, and format specifiers for printing values using `printf()`.

| **Type**                   | **Typical Size (Bits)** | **Minimal Range**                     | **Format Specifier** |
|----------------------------|-------------------------|---------------------------------------|----------------------|
| `char`                     | 8                       | -128 to 127                           | `%c`                 |
| `unsigned char`            | 8                       | 0 to 255                              | `%c`                 |
| `signed char`              | 8                       | -128 to 127                           | `%c`                 |
| `int`                      | 16 or 32                | -32,768 to 32,767                     | `%d`, `%i`           |
| `unsigned int`             | 16 or 32                | 0 to 65,535                           | `%u`                 |
| `signed int`               | 16 or 32                | Same as `int`                         | `%d`, `%i`           |
| `short int`                | 16                      | -32,768 to 32,767                     | `%hd`                |
| `unsigned short int`       | 16                      | 0 to 65,535                           | `%hu`                |
| `signed short int`         | 16                      | Same as `short int`                   | `%hd`                |
| `long int`                 | 32                      | -2,147,483,648 to 2,147,483,647       | `%ld`, `%li`         |
| `long long int`            | 64                      | -(2^63 - 1) to 2^63 - 1              | `%lld`, `%lli`       |
| `signed long int`          | 32                      | Same as `long int`                    | `%ld`, `%li`         |
| `unsigned long int`        | 32                      | 0 to 4,294,967,295                    | `%lu`                |
| `unsigned long long int`   | 64                      | 0 to 2^64 - 1                         | `%llu`               |
| `float`                    | 32                      | 1E-37 to 1E+37 (6 digits precision)   | `%f`                 |
| `double`                   | 64                      | 1E-37 to 1E+37 (10 digits precision)  | `%lf`                |
| `long double`              | 80                      | 1E-37 to 1E+37 (10 digits precision)  | `%Lf`                |

### Out-of-Range Values
- Assigning a value outside the allowed range may cause:
  - Compilation error or warning, depending on the compiler.
  - Undefined behavior or data overflow.

## Program to Display Data Type Sizes


**Note**: Output varies by system architecture and compiler.
```c
#include <stdio.h>
int main() {
    printf("Size of Integer: %ld \n", sizeof(int));
    printf("Size of Character: %ld \n", sizeof(char));
    printf("Size of Float: %ld \n", sizeof(float));
    printf("Size of Double: %ld \n", sizeof(double));
    printf("Size of Signed Integer: %ld \n", sizeof(signed int));
    printf("Size of Signed Character: %ld \n", sizeof(signed char));
    printf("Size of Unsigned Integer: %ld \n", sizeof(unsigned int));
    printf("Size of Unsigned Character: %ld \n", sizeof(unsigned char));
    printf("Size of Long Integer: %ld \n", sizeof(long int));
    printf("Size of Long Double: %ld \n", sizeof(long double));
    return 0;
}
```

## Primary Data Type Declaration and Initialization
Some compilers require initialization during declaration. Recommended initial values for best practices:

| **Data Type** | **Initial Value** |
|---------------|-------------------|
| `int`         | 0                 |
| `char`        | `'\0'`           |
| `float`       | 0                 |
| `double`      | 0                 |
| `void`        | Nothing           |

- Initial values can be changed based on the problem being solved.

## Key Points
- C supports five primary data types: `char`, `int`, `float`, `double`, and `void`.
- Data type sizes depend on the compiler and processor architecture.
- Modifiers (`signed`, `unsigned`, `long`, `short`) adjust the range and behavior of data types.
- Signed types use a sign bit, reducing the range compared to unsigned types.
- Use appropriate format specifiers in `printf()` to display values.
- Out-of-range values may cause errors or undefined behavior.
- Initialization of variables is a good practice for code reliability.

**Note**: The section on operators was not provided in the input. If you provide details on operators, I can include them in an updated version of these notes.