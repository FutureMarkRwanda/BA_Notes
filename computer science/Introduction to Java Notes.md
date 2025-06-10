# Unit 10: Introduction to Java

## 10.1 Concepts of Java Programming
Java is a versatile, object-oriented programming language designed for portability and robustness.

- **What is Java?**
  - A high-level, platform-independent language developed by Sun Microsystems (now Oracle).
  - Used for web, mobile, desktop, and enterprise applications.
  - Known for its “write once, run anywhere” (WORA) principle.
- **Key Concepts**:
  - **Object-Oriented**: Organizes code around objects (data + behavior), supporting encapsulation, inheritance, polymorphism, and abstraction.
  - **Platform-Independent**: Java code runs on any device with a Java Virtual Machine (JVM).
  - **Robust**: Strong type-checking, exception handling, and automatic memory management (garbage collection).
  - **Secure**: Features like bytecode verification and sandboxing enhance security.
- **Applications**:
  - Web applications (e.g., servlets, JSP).
  - Mobile apps (e.g., Android development).
  - Enterprise systems (e.g., banking software).
- **Example Concept**:
  - Think of Java as a universal recipe book. You write a recipe (code) once, and it can be used in any kitchen (platform) with a Java interpreter (JVM).
- **Self-Study Tip**:
  - Java’s strength is its portability. Imagine writing a game that runs on both a PC and a phone without changing the code.

## 10.2 Platforms of Java Program
Java supports multiple platforms, enabling applications to run across diverse environments.

- **What are Java Platforms?**
  - Editions of Java tailored for specific purposes, each including the JVM and libraries.
- **Main Platforms**:
  - **Java SE (Standard Edition)**:
    - For desktop and standalone applications.
    - Includes core libraries (e.g., `java.lang`, `java.util`).
    - Example: A calculator app.
  - **Java EE (Enterprise Edition)**:
    - For large-scale, distributed systems (e.g., web servers).
    - Includes APIs for web services, databases (e.g., JDBC, JPA).
  - **Java ME (Micro Edition)**:
    - For resource-constrained devices (e.g., older mobile phones).
    - Lightweight libraries for embedded systems.
  - **JavaFX**: For rich GUI applications (modern replacement for Swing).
  - **Android**: Uses Java (or Kotlin) with Android-specific libraries.
- **Role of JVM**:
  - The Java Virtual Machine interprets compiled Java code (bytecode) to run on any platform (Windows, Linux, macOS).
  - Example: A Java program written on Windows runs on Linux without modification.
- **Self-Study Tip**:
  - Think of platforms as different toolkits. Java SE is like a basic toolbox for general tasks, while Java EE is a specialized kit for big projects.

## 10.3 Write, Compile, and Run a Java Program
Creating a Java program involves writing code, compiling it into bytecode, and running it on the JVM.

- **Steps Overview**:
  1. Write the Java source code in a `.java` file.
  2. Compile the code into bytecode (`.class` file) using the `javac` compiler.
  3. Run the bytecode using the `java` command.
- **Example (Simple Program)**:
  ```java
  public class HelloWorld {
      public static void main(String[] args) {
          System.out.println("Hello, Java!");
      }
  }
  ```
  - Save as `HelloWorld.java` (file name must match class name).
- **Self-Study Tip**:
  - Writing a Java program is like writing a letter, compiling is like translating it into a universal code, and running is like delivering it to the reader (JVM).

## 10.4 Compile the Source File into a .class File
Compiling converts human-readable Java code into machine-readable bytecode.

- **What is Compilation?**
  - The `javac` command processes a `.java` file to produce a `.class` file containing bytecode.
  - Bytecode is platform-independent and executed by the JVM.
- **Steps to Compile**:
  1. Ensure the Java Development Kit (JDK) is installed.
  2. Open a terminal/command prompt.
  3. Navigate to the directory containing `HelloWorld.java`.
  4. Run: `javac HelloWorld.java`
  5. Output: A `HelloWorld.class` file is created.
- **Common Errors**:
  - Syntax errors (e.g., missing semicolon `;`).
  - File name mismatch (e.g., `HelloWorld.java` must match `public class HelloWorld`).
- **Example**:
  - Command: `javac HelloWorld.java`
  - Result: Creates `HelloWorld.class` if no errors.
- **Self-Study Tip**:
  - Compilation is like baking a cake. The recipe (`.java`) is turned into a finished cake (`.class`) that the JVM can “eat” (execute).

## 10.5 Running the Program
Running a Java program executes the compiled bytecode on the JVM.

- **How to Run?**
  - Use the `java` command to execute the `.class` file.
  - Syntax: `java ClassName` (omit `.class` extension).
- **Steps**:
  1. Ensure the `.class` file exists (from compilation).
  2. In the terminal, run: `java HelloWorld`
  3. Output: `Hello, Java!` (from the example above).
- **Main Method**:
  - The `public static void main(String[] args)` method is the entry point for Java programs.
  - Must be present in the class you run.
- **Common Issues**:
  - `NoClassDefFoundError`: `.class` file not found (check directory or classpath).
  - `Main method not found`: Ensure the `main` method is correctly defined.
- **Example**:
  - Command: `java HelloWorld`
  - Output: `Hello, Java!`
- **Self-Study Tip**:
  - Running a program is like pressing “play” on a music player. The JVM reads the bytecode (song) and produces output (music).

## 10.6 Elements of Java Source File
A Java source file (`.java`) follows a specific structure with key components.

- **Key Elements**:
  - **Class Declaration**:
    - Defines a class using `class ClassName`.
    - Example: `public class MyProgram { ... }`.
  - **Main Method**:
    - Entry point: `public static void main(String[] args)`.
    - Required to run the program.
  - **Imports**:
    - Import libraries (e.g., `import java.util.Scanner;` for user input).
    - Placed at the top of the file.
  - **Variables and Methods**:
    - Variables store data (e.g., `int x = 5;`).
    - Methods define behavior (e.g., `void display() { ... }`).
  - **Comments**:
    - Single-line: `// Comment`
    - Multi-line: `/* Comment */`
- **Rules**:
  - File name must match the `public` class name (e.g., `MyProgram.java` for `public class MyProgram`).
  - Only one `public` class per file.
- **Example**:
  ```java
  // Import statement
  import java.util.Scanner;
  // Class declaration
  public class MyProgram {
      // Main method
      public static void main(String[] args) {
          // Variable
          int number;
          // Object for user input
          Scanner scanner = new Scanner(System.in);
          System.out.print("Enter a number: ");
          number = scanner.nextInt();
          // Method call
          displayResult(number);
          scanner.close();
      }
      // Custom method
      static void displayResult(int num) {
          System.out.println("You entered: " + num);
      }
  }
  ```
- **Self-Study Tip**:
  - A Java source file is like a blueprint for a house. The class is the structure, the main method is the front door, and imports bring in tools (libraries).

## 10.7 Flow Control
Flow control structures manage the execution order of code based on conditions or repetition.

- **What is Flow Control?**
  - Mechanisms to control program flow using decision-making (conditionals) and repetition (loops).
- **Decision Structures**:
  - **if Statement**:
    - Executes code if a condition is true.
    - Syntax: `if (condition) { ... }`
    - Example:
      ```java
      int x = 10;
      if (x > 5) {
          System.out.println("x is greater than 5");
      }
      ```
  - **if-else Statement**:
    - Handles true and false outcomes.
    - Example:
      ```java
      int age = 16;
      if (age >= 18) {
          System.out.println("Adult");
      } else {
          System.out.println("Minor");
      }
      ```
  - **else if Ladder**:
    - Checks multiple conditions.
    - Example:
      ```java
      int score = 85;
      if (score >= 90) {
          System.out.println("Grade A");
      } else if (score >= 80) {
          System.out.println("Grade B");
      } else {
          System.out.println("Below B");
      }
      ```
  - **switch Statement**:
    - Selects code based on a variable’s value.
    - Example:
      ```java
      int day = 2;
      switch (day) {
          case 1:
              System.out.println("Monday");
              break;
          case 2:
              System.out.println("Tuesday");
              break;
          default:
              System.out.println("Other day");
      }
      ```
- **Repetition Structures (Loops)**:
  - **for Loop**:
    - Loops a fixed number of times.
    - Syntax: `for (init; condition; update) { ... }`
    - Example:
      ```java
      for (int i = 1; i <= 3; i++) {
          System.out.println("Count: " + i);
      }
      ```
  - **while Loop**:
    - Loops while a condition is true.
    - Example:
      ```java
      int count = 1;
      while (count <= 3) {
          System.out.println("Count: " + count);
          count++;
      }
      ```
  - **do-while Loop**:
    - Loops at least once, checks condition at the end.
    - Example:
      ```java
      int num = 1;
      do {
          System.out.println("Number: " + num);
          num++;
      } while (num <= 3);
      ```
- **Self-Study Tip**:
  - Flow control is like navigating a maze. Conditionals (if/switch) choose paths based on signs (conditions), and loops (for/while) repeat steps until you reach a goal.