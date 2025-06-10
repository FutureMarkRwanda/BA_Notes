# Chapter 3: C Operators

## Overview of Operators
- **Definition**: Symbols that instruct the compiler to perform mathematical, logical, or other operations.
- **Types**: Arithmetic, Relational, Logical, Bitwise, Assignment, Miscellaneous.

## Arithmetic Operators
Perform mathematical operations. Assume `A = 10`, `B = 20`.

| **Operator** | **Description**                              | **Example**         |
|--------------|----------------------------------------------|---------------------|
| `+`          | Adds two operands                            | `A + B = 30`        |
| `-`          | Subtracts second operand from first          | `A - B = -10`       |
| `*`          | Multiplies both operands                     | `A * B = 200`       |
| `/`          | Divides numerator by denominator             | `B / A = 2`         |
| `%`          | Modulus: remainder of integer division       | `B % A = 0`         |
| `++`         | Increments value by one                      | `A++ = 11`          |
| `--`         | Decrements value by one                      | `A-- = 9`           |

## Relational (Comparison) Operators
Compare two operands. Assume `A = 10`, `B = 20`.

| **Operator** | **Description**                              | **Example**         |
|--------------|----------------------------------------------|---------------------|
| `==`         | Checks if operands are equal                 | `(A == B)` is false |
| `!=`         | Checks if operands are not equal             | `(A != B)` is true  |
| `>`          | Checks if left operand is greater            | `(A > B)` is false  |
| `<`          | Checks if left operand is less               | `(A < B)` is true   |
| `>=`         | Checks if left operand is greater or equal   | `(A >= B)` is false |
| `<=`         | Checks if left operand is less or equal      | `(A <= B)` is true  |

### Example Program: Find Greatest of Three Numbers
```c
#include <stdio.h>
int main() {
    int a, b, c;
    printf("Enter three numbers: ");
    scanf("%d %d %d", &a, &b, &c);
    if (a > b && a > c) {
        printf("%d is the greatest\n", a);
    } else if (b > a && b > c) {
        printf("%d is the greatest\n", b);
    } else {
        printf("%d is the greatest\n", c);
    }
    return 0;
}
```

## Logical Operators
Combine or negate conditions. Assume `A = 1`, `B = 0`.

| **Operator** | **Description**                              | **Example**         |
|--------------|----------------------------------------------|---------------------|
| `&&`         | Logical AND: true if both operands are true  | `(A && B)` is false |
| `||`         | Logical OR: true if either operand is true   | `(A || B)` is true  |
| `!`          | Logical NOT: reverses operand's logical state | `!(A && B)` is true |

### Assignment: Modify Greatest Number Program with Logical Operators
The example above already uses `&&` to compare numbers. To enhance, you could add conditions like:
```c
if (a > b && a > c && a != b && a != c) {
    printf("%d is the greatest and unique\n", a);
}
```

## Bitwise Operators
Operate on bits. Assume `A = 60 (0011 1100)`, `B = 13 (0000 1101)`.

| **Operator** | **Description**                              | **Example**                     |
|--------------|----------------------------------------------|---------------------------------|
| `&`          | Binary AND: copies bit if in both operands   | `(A & B) = 12 (0000 1100)`      |
| `|`          | Binary OR: copies bit if in either operand   | `(A | B) = 61 (0011 1101)`      |
| `^`          | Binary XOR: copies bit if set in one operand | `(A ^ B) = 49 (0011 0001)`      |
| `~`          | Binary One's Complement: flips bits          | `(~A) = -61 (1100 0011)`        |
| `<<`         | Left Shift: shifts bits left                 | `(A << 2) = 240 (1111 0000)`    |
| `>>`         | Right Shift: shifts bits right               | `(A >> 2) = 15 (0000 1111)`     |

**Truth Table** for `&`, `|`, `^`:

| **p** | **q** | **p & q** | **p \| q** | **p ^ q** |
|-------|-------|-----------|------------|-----------|
| 0     | 0     | 0         | 0          | 0         |
| 0     | 1     | 0         | 1          | 1         |
| 1     | 1     | 1         | 1          | 0         |
| 1     | 0     | 0         | 1          | 1         |

## Assignment Operators
Assign values or perform operations and assign results.

| **Operator** | **Description**                              | **Example**                     |
|--------------|----------------------------------------------|---------------------------------|
| `=`          | Assigns right operand to left operand        | `C = A + B`                     |
| `+=`         | Adds right operand to left and assigns       | `C += A` ≡ `C = C + A`          |
| `-=`         | Subtracts right operand and assigns          | `C -= A` ≡ `C = C - A`          |
| `*=`         | Multiplies right operand and assigns         | `C *= A` ≡ `C = C * A`          |
| `/=`         | Divides left by right operand and assigns    | `C /= A` ≡ `C = C / A`          |
| `%=`         | Modulus and assigns                          | `C %= A` ≡ `C = C % A`          |
| `<<=`        | Left shift and assigns                       | `C <<= 2` ≡ `C = C << 2`        |
| `>>=`        | Right shift and assigns                      | `C >>= 2` ≡ `C = C >> 2`        |
| `&=`         | Bitwise AND and assigns                      | `C &= 2` ≡ `C = C & 2`          |
| `^=`         | Bitwise XOR and assigns                      | `C ^= 2` ≡ `C = C ^ 2`          |
| `|=`         | Bitwise OR and assigns                       | `C |= 2` ≡ `C = C | 2`          |

## Miscellaneous Operators
Additional operators for specific tasks.

| **Operator** | **Description**                              | **Example**                     |
|--------------|----------------------------------------------|---------------------------------|
| `sizeof()`   | Returns size of a variable                   | `sizeof(int)` returns 4         |
| `&`          | Returns address of a variable                | `&a` returns variable address   |
| `*`          | Pointer to a variable                        | `*a` accesses value at address  |
| `?:`         | Conditional (ternary): `condition ? val1 : val2` | `(a > b) ? b : a` returns 9 |

**Ternary Example**:
```c
int a = 9, b = 12;
int x = (a > b) ? b : a; // x = 9, since a > b is false
```

## Operator Precedence
Determines the order of evaluation in expressions. Higher precedence operators are evaluated first.

| **Category**       | **Operators**                     | **Associativity** |
|--------------------|-----------------------------------|-------------------|
| Postfix            | `() [] -> . ++ --`                | Left to right     |
| Unary              | `+ - ! ~ ++ -- (type) * & sizeof` | Right to left     |
| Multiplicative     | `* / %`                           | Left to right     |
| Additive           | `+ -`                             | Left to right     |
| Shift              | `<< >>`                           | Left to right     |
| Relational         | `< <= > >=`                       | Left to right     |
| Equality           | `== !=`                           | Left to right     |
| Bitwise AND        | `&`                               | Left to right     |
| Bitwise XOR        | `^`                               | Left to right     |
| Bitwise OR         | `|`                               | Left to right     |
| Logical AND        | `&&`                              | Left to right     |
| Logical OR         | `||`                              | Left to right     |
| Conditional        | `?:`                              | Right to left     |
| Assignment         | `= += -= *= /= %= >>= <<= &= ^= |=`| Right to left     |
| Comma              | `,`                               | Left to right     |

**Example**:
```c
int x = 7 + 3 * 2; // x = 13, not 20, since * has higher precedence than +
```

## Key Points
- Operators enable mathematical, logical, and bitwise operations in C.
- Arithmetic operators handle basic math; relational operators compare values.
- Logical operators combine conditions; bitwise operators manipulate bits.
- Assignment operators streamline value updates; miscellaneous operators handle special cases like pointers and conditionals.
- Operator precedence governs expression evaluation order, critical for correct results.