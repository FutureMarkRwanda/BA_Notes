# Unit 12: IO and Java

## 12.1 Introduction to IO Streams
Input/Output (I/O) streams in Java handle data transfer, such as reading from files or writing to the console.

- **What are IO Streams?**
  - Streams are sequences of data (bytes or characters) that flow from a source (e.g., file, keyboard) to a destination (e.g., file, screen).
  - Java’s I/O system is provided by the `java.io` package.
- **Types of Streams**:
  - **Byte Streams**: Handle raw binary data (e.g., images, files) using classes like `InputStream` and `OutputStream`.
  - **Character Streams**: Handle text data (e.g., strings) using classes like `Reader` and `Writer`.
- **Key Concepts**:
  - **Input**: Reading data into a program (e.g., from a file).
  - **Output**: Writing data from a program (e.g., to a file or console).
  - Streams often use buffering to improve efficiency.
- **Example Concept**:
  - Reading a file is like drinking water from a straw (stream) from a glass (source). Writing is like pouring water into a glass (destination).
- **Self-Study Tip**:
  - Think of streams as pipes carrying data. Byte streams carry raw data (like water), and character streams carry text (like labeled bottles).

## 12.2 InputStream, OutputStream, and FileStream
Byte streams handle raw binary data, with `InputStream` and `OutputStream` as base classes, and `FileInputStream` and `FileOutputStream` for file operations.

- **InputStream**:
  - Abstract class for reading bytes from a source (e.g., file, network).
  - Key method: `read()` (reads a byte or array of bytes).
- **OutputStream**:
  - Abstract class for writing bytes to a destination.
  - Key method: `write()` (writes a byte or array of bytes).
- **FileInputStream and FileOutputStream**:
  - Subclasses for reading from and writing to files.
  - Used for binary data like images or raw text.
- **Key Points**:
  - Always close streams using `close()` to free resources.
  - Use try-catch for handling `IOException` (e.g., file not found).
- **Self-Study Tip**:
  - Byte streams are like moving raw materials (bytes) through a conveyor belt. `FileInputStream` pulls materials in, and `FileOutputStream` sends them out.
- **Example (Reading and Writing a File)**:
  ```java
  import java.io.*;
  public class Main {
      public static void main(String[] args) {
          try {
              // Writing to a file
              FileOutputStream fos = new FileOutputStream("output.txt");
              String text = "Hello, Java!";
              fos.write(text.getBytes()); // Convert string to bytes
              fos.close();
              // Reading from a file
              FileInputStream fis = new FileInputStream("output.txt");
              int data;
              while ((data = fis.read()) != -1) { // Read byte by byte
                  System.out.print((char) data); // Output: Hello, Java!
              }
              fis.close();
          } catch (IOException e) {
              System.out.println("Error: " + e.getMessage());
          }
      }
  }
  ```

## 12.3 File Streams (File Operations)
This section extends file stream operations, focusing on practical file reading and writing using `FileInputStream` and `FileOutputStream`.

- **File Stream Operations**:
  - **Reading**: Use `FileInputStream` to read bytes from a file.
  - **Writing**: Use `FileOutputStream` to write bytes to a file.
  - **Common Methods**:
    - `read(byte[] buffer)`: Reads bytes into a buffer.
    - `write(byte[] buffer)`: Writes a buffer of bytes.
- **Example (Using Buffers for Efficiency)**:
  ```java
  import java.io.*;
  public class Main {
      public static void main(String[] args) {
          try {
              // Writing to a file
              FileOutputStream fos = new FileOutputStream("data.txt");
              String text = "Java I/O is fun!";
              byte[] buffer = text.getBytes();
              fos.write(buffer);
              fos.close();
              // Reading from a file
              FileInputStream fis = new FileInputStream("data.txt");
              byte[] readBuffer = new byte[1024]; // Buffer for reading
              int bytesRead = fis.read(readBuffer);
              String content = new String(readBuffer, 0, bytesRead);
              System.out.println(content); // Output: Java I/O is fun!
              fis.close();
          } catch (IOException e) {
              System.out.println("Error: " + e.getMessage());
          }
      }
  }
  ```
- **Best Practices**:
  - Use buffers to reduce direct disk access, improving performance.
  - Handle exceptions to manage errors like missing files.
  - Consider `try-with-resources` to auto-close streams (introduced in Java 7).
- **Example (try-with-resources)**:
  ```java
  import java.io.*;
  public class Main {
      public static void main(String[] args) {
          try (FileOutputStream fos = new FileOutputStream("test.txt")) {
              fos.write("Auto-close example".getBytes());
          } catch (IOException e) {
              System.out.println("Error: " + e.getMessage());
          }
      }
  }
  ```
- **Self-Study Tip**:
  - File streams are like a librarian moving books (data) to and from shelves (files). Buffers are like a cart to carry multiple books at once.

## 12.4 Readers and Writers
Readers and Writers handle character-based data (text), providing a higher-level abstraction than byte streams.

- **What are Readers and Writers?**
  - Classes in `java.io` for reading and writing character data (Unicode).
  - Base classes: `Reader` (for input) and `Writer` (for output).
- **Common Classes**:
  - **FileReader**: Reads characters from a file.
  - **FileWriter**: Writes characters to a file.
  - **BufferedReader**: Reads text efficiently using a buffer.
  - **BufferedWriter**: Writes text efficiently using a buffer.
- **Example (Reading and Writing Text)**:
  ```java
  import java.io.*;
  public class Main {
      public static void main(String[] args) {
          try {
              // Writing to a file
              FileWriter fw = new FileWriter("text.txt");
              fw.write("Welcome to Java I/O");
              fw.close();
              // Reading from a file
              FileReader fr = new FileReader("text.txt");
              int ch;
              while ((ch = fr.read()) != -1) { // Read character by character
                  System.out.print((char) ch); // Output: Welcome to Java I/O
              }
              fr.close();
          } catch (IOException e) {
              System.out.println("Error: " + e.getMessage());
          }
      }
  }
  ```
- **BufferedReader/BufferedWriter Example**:
  ```java
  import java.io.*;
  public class Main {
      public static void main(String[] args) {
          try {
              // Writing with BufferedWriter
              BufferedWriter bw = new BufferedWriter(new FileWriter("buffer.txt"));
              bw.write("Buffered writing");
              bw.newLine(); // Add newline
              bw.write("Line 2");
              bw.close();
              // Reading with BufferedReader
              BufferedReader br = new BufferedReader(new FileReader("buffer.txt"));
              String line;
              while ((line = br.readLine()) != null) {
                  System.out.println(line); // Output: Buffered writing, Line 2
              }
              br.close();
          } catch (IOException e) {
              System.out.println("Error: " + e.getMessage());
          }
      }
  }
  ```
- **Self-Study Tip**:
  - Readers and Writers are like reading and writing letters (text), while Buffered classes are like using a notepad to collect lines before mailing or reading them.

## 12.5 Character Stream
Character streams specifically handle text data, using Unicode to support international characters.

- **What is a Character Stream?**
  - A stream designed for text data, processing 16-bit Unicode characters.
  - Unlike byte streams, character streams handle text encoding automatically.
- **Key Classes**:
  - `FileReader`, `FileWriter`: Basic text file operations.
  - `BufferedReader`, `BufferedWriter`: Efficient text operations with buffering.
  - `InputStreamReader`, `OutputStreamWriter`: Bridge byte streams to character streams, specifying encoding (e.g., UTF-8).
- **Why Use Character Streams?**
  - Ideal for text files (e.g., `.txt`, `.csv`).
  - Handle encoding issues (e.g., UTF-8, ASCII) transparently.
  - More convenient than byte streams for text processing.
- **Self-Study Tip**:
  - Character streams are like a translator who converts raw data (bytes) into readable text, making it easier to work with words and sentences.


- **Example (Using InputStreamReader)**:
  ```java
  import java.io.*;
  public class Main {
      public static void main(String[] args) {
          try {
              // Convert byte stream to character stream
              InputStreamReader isr = new InputStreamReader(new FileInputStream("text.txt"), "UTF-8");
              int ch;
              while ((ch = isr.read()) != -1) {
                  System.out.print((char) ch);
              }
              isr.close();
          } catch (IOException e) {
              System.out.println("Error: " + e.getMessage());
          }
      }
  }
  ```
