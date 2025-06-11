# Multiple Choice Quiz: IO and Java

1. What is an I/O stream in Java?
   - A) A loop structure
   - B) A sequence of data for input/output
   - C) A data type
   - D) A class method
   
2. Which package provides Java I/O classes?
   - A) java.util
   - B) java.io
   - C) java.net
   - D) java.lang
   
3. What type of data does `InputStream` handle?
   - A) Characters
   - B) Bytes
   - C) Objects
   - D) Strings
   
4. Which class is used to read bytes from a file?
   - A) FileReader
   - B) FileInputStream
   - C) BufferedWriter
   - D) OutputStream
   
5. What method reads a single byte from an `InputStream`?
   - A) write()
   - B) read()
   - C) close()
   - D) flush()
   
6. Which class writes bytes to a file?
   - A) FileWriter
   - B) FileOutputStream
   - C) BufferedReader
   - D) InputStream
   
7. Why should you close a stream in Java?
   - A) To increase performance
   - B) To free system resources
   - C) To read data
   - D) To compile the program
   
8. What exception is commonly handled in I/O operations?
   - A) NullPointerException
   - B) IOException
   - C) ArrayIndexOutOfBoundsException
   - D) ClassNotFoundException
   
9. Which feature auto-closes streams in Java 7+?
   - A) try-catch
   - B) try-with-resources
   - C) finally
   - D) close()
   
10. What is the benefit of using buffers in file operations?
    - A) Increases file size
    - B) Improves performance
    - C) Changes encoding
    - D) Prevents errors
    
11. Which class is used to read character data from a file?
    - A) FileInputStream
    - B) FileReader
    - C) OutputStream
    - D) BufferedWriter
    
12. Which class provides efficient text reading with buffering?
    - A) FileWriter
    - B) BufferedReader
    - C) InputStreamReader
    - D) FileOutputStream
    
13. What does `BufferedReader.readLine()` do?
    - A) Reads a single character
    - B) Reads a line of text
    - C) Writes a line
    - D) Closes the stream
    
14. Which class writes character data to a file?
    - A) FileOutputStream
    - B) FileWriter
    - C) BufferedReader
    - D) InputStream
    
15. What is true about character streams?
    - A) They handle binary data
    - B) They process Unicode text
    - C) They are slower than byte streams
    - D) They cannot use buffers
    
16. Which class bridges byte streams to character streams?
    - A) FileReader
    - B) InputStreamReader
    - C) FileOutputStream
    - D) BufferedWriter
    
17. What encoding is commonly used with character streams?
    - A) Binary
    - B) UTF-8
    - C) ASCII-128
    - D) Bytecode
    
18. What does the `write()` method of `FileOutputStream` do?
    - A) Reads bytes
    - B) Writes bytes
    - C) Closes the stream
    - D) Buffers data
    
19. What is the output of this code if "test.txt" contains "Hello"? `FileReader fr = new FileReader("test.txt"); int ch = fr.read(); System.out.print((char) ch);`
    - A) Hello
    - B) H
    - C) Error
    - D) Nothing

20. Which class is used to write text efficiently with buffering?
    - A) FileReader
    - B) FileOutputStream
    - C) BufferedWriter
    - D) InputStreamReader

21. What does `BufferedWriter.newLine()` do?
    - A) Reads a line
    - B) Writes a newline character
    - C) Closes the stream
    - D) Clears the buffer

22. Why are character streams preferred for text files?
    - A) They are faster than byte streams
    - B) They handle text encoding automatically
    - C) They support binary data
    - D) They require no buffering
