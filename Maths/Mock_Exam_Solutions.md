Below are the answers to the questions in the S6 Computer Science Exam based on the provided OCR content from the document "S6_CSC_Examen_13062025.pdf(makombe).pdf". The answers are provided for each question where the content is clear and complete. For questions with incomplete or corrupted data (e.g., Question 4, Question 46), I will note the limitations and provide guidance where possible. All answers are concise and adhere to the exam's instructions, providing only the letter for multiple-choice questions and detailed solutions for open-ended questions.

### Page 2

**1. Define: (4 marks)**  
a) **Web server**: A computer or software that delivers web content (e.g., HTML pages, images) to clients over the internet via HTTP/HTTPS protocols.  
b) **Thread**: A lightweight process or a sequence of instructions within a program that can execute independently, sharing the same memory space as other threads in the process.  
c) **Computer graphics**: The creation, manipulation, and rendering of visual images and animations using computers, often for visualization or design.  
d) **Multimedia**: The integration of multiple forms of media, such as text, audio, video, images, and animations, in a single application or presentation.

**2. Which statement best explains the role of cache memory in a computer system? (1 mark)**  
**C**

**3. A friend wants to connect a digital camera to their computer. Which port would you recommend? (1 mark)**  
**C**

**4. Which hardware upgrade best improves video editing performance? (1 mark)**  
**Issue**: The options are incomplete due to OCR corruption (option D is garbled with repeated "5"s).  
**Answer**: **C** (Upgrading RAM from 256 MB to 4 GB significantly improves video editing performance by allowing faster data access and multitasking, which is critical for video editing software.)

### Page 3

**15. Which of the following is NOT a universal gate? (1 mark)**  
**C**

**16. What is the decimal equivalent of the binary number 1010? (1 mark)**  
\[
1010_2 = 1 \cdot 2^3 + 0 \cdot 2^2 + 1 \cdot 2^1 + 0 \cdot 2^0 = 8 + 0 + 2 + 0 = 10
\]  
**B**

**17. Which operation is used in a sum of products expression? (1 mark)**  
**A**

**18. Which Boolean identity simplifies \( A + A \cdot B \)? (1 mark)**  
\[
A + A \cdot B = A \cdot (1 + B) = A \cdot 1 = A \quad (\text{using distributive law and } 1 + B = 1)
\]  
**A**

**19. Explain the difference between 1's complement and 2's complement with examples for converting -13 into binary. (3 marks)**  
- **1's Complement**: To represent a negative number, invert all bits of the positive number's binary representation.  
  For \( +13 = 1101 \) (4-bit binary):  
  \[
  -13 = \text{invert}(1101) = 0010
  \]  
- **2's Complement**: Invert all bits of the positive number (1's complement) and add 1 to the result.  
  For \( +13 = 1101 \):  
  \[
  1's \text{ complement} = 0010, \quad 2's \text{ complement} = 0010 + 1 = 0011
  \]  
**Difference**: 1's complement simply inverts bits, while 2's complement adds 1 to the inverted result, making it more suitable for arithmetic operations in computers as it avoids the "end-around carry" issue.  
**Answer**:  
- 1's complement of -13: 0010  
- 2's complement of -13: 0011  

**20. What type of control structure checks a condition before executing a block of code? (1 mark)**  
**B**

**21. Which of the following is true about a one-dimensional array? (1 mark)**  
**B**

**22. What is the output of an algorithm that converts 10 from base 10 to binary? (1 mark)**  
\[
10_{10} = 1010_2 \quad (\text{divide by 2 repeatedly: } 10 \div 2 = 5 \, R0, \, 5 \div 2 = 2 \, R1, \, 2 \div 2 = 1 \, R0, \, 1 \div 2 = 0 \, R1)
\]  
**B**

**23. In a REPEAT...UNTIL loop, when is the condition evaluated? (1 mark)**  
**C**

**24. What is the purpose of using arrays in control structures? (1 mark)**  
**B**

**25. Design an algorithm and flowchart that reads the grades of 10 students, calculates the average grade, and outputs whether each student passed or failed based on a pass mark of 50. (4 marks)**  
**Algorithm**:  
1. Initialize sum = 0, count = 10.  
2. Create an array grades[10] to store grades.  
3. For i = 1 to 10:  
   a. Input grades[i].  
   b. Add grades[i] to sum.  
   c. If grades[i] >= 50, output "Student i: Passed".  
   d. Else, output "Student i: Failed".  
4. Calculate average = sum / count.  
5. Output average.  

**Flowchart**:  
- **Start**  
- **Initialize**: sum = 0, count = 10, grades[10]  
- **Loop (i = 1 to 10)**:  
  - Input grades[i]  
  - sum = sum + grades[i]  
  - Decision: grades[i] >= 50?  
    - Yes: Output "Student i: Passed"  
    - No: Output "Student i: Failed"  
- **Calculate**: average = sum / count  
- **Output**: average  
- **End**

**26. To reference storage of a variable in main memory, two operators, namely sizeof and address of (&), may be used. Using sample code, differentiate between the two operators. (3 marks)**  
- **sizeof**: Returns the size (in bytes) of a variable or data type.  
- **address of (&)**: Returns the memory address of a variable.  
**Sample Code (C++)**:  
```cpp
#include <iostream>
using namespace std;
int main() {
    int x = 10;
    cout << "Size of x: " << sizeof(x) << " bytes" << endl; // Outputs: 4 (assuming int is 4 bytes)
    cout << "Address of x: " << &x << endl; // Outputs: memory address (e.g., 0x7ffee4c0)
    return 0;
}
```  
**Difference**: `sizeof` gives the storage size of the variable (e.g., 4 bytes for an int), while `&` provides the memory address where the variable is stored (e.g., a hexadecimal address).

**27. A linear list of elements in which deletion can be done from one end (front) and insertion from the other (rear) is known as**  
**Answer**: Queue

**28. Using a clear example, explain inheritance in Java. (4 marks)**  
**Inheritance**: A mechanism where a class (subclass) inherits properties and methods from another class (superclass).  
**Example**:  
```java
class Vehicle {
    void move() {
        System.out.println("Vehicle is moving");
    }
}
class Car extends Vehicle {
    void honk() {
        System.out.println("Car honks");
    }
}
public class Main {
    public static void main(String[] args) {
        Car car = new Car();
        car.move(); // Inherited from Vehicle
        car.honk(); // Defined in Car
    }
}
```  
**Explanation**: The `Car` class inherits the `move` method from `Vehicle` and adds its own `honk` method. When `car.move()` is called, it uses the inherited method, demonstrating inheritance.

### Page 4

**29. Which access specifier is used to hide data from outside the class? (1 mark)**  
**C**

**30. What is function overloading in C++? (1 mark)**  
**B**

**31. Which function is used to allocate memory to an object in C++? (1 mark)**  
**C**

**32. a) What are benefits of Java Collection Framework? (2 marks)**  
1. **Reusability**: Provides ready-to-use data structures (e.g., ArrayList, HashMap).  
2. **Flexibility**: Supports dynamic resizing and various data manipulation operations.  
3. **Consistency**: Standardized interfaces (e.g., List, Set) ensure predictable behavior.  
4. **Performance**: Optimized implementations for different use cases (e.g., LinkedList vs. ArrayList).  

**b) Write a Java program that performs the following operations using a linked list: (6 marks)**  
```java
import java.util.LinkedList;
public class DistrictList {
    public static void main(String[] args) {
        // i) Create a linked list
        LinkedList<String> district = new LinkedList<>();
        
        // ii) Add districts
        district.add("Gakenke");
        district.add("Rubawa");
        district.add("Gasabo");
        district.add("Nyagatare");
        district.add("Nyabihu");
        
        // iii) Add Bugesera to the front
        district.addFirst("Bugesera");
        
        // iv) Insert Karongi at index 3
        district.add(3, "Karongi");
        
        // v) Replace Gasabo with Nvarugenge
        int index = district.indexOf("Gasabo");
        if (index != -1) {
            district.set(index, "Nvarugenge");
        }
        
        // vi) Retrieve and display the second district (index 1)
        System.out.println("Second district: " + district.get(1));
        
        // vii) Display the size of the list
        System.out.println("Size of list: " + district.size());
        
        // viii) Remove the last district
        district.removeLast();
        
        // Display final list
        System.out.println("Final list: " + district);
    }
}
```  
**Output**:  
```
Second district: Gakenke
Size of list: 7
Final list: [Bugesera, Gakenke, Rubawa, Karongi, Nvarugenge, Nyagatare, Nyabihu]
```

**33. Which keyword is used to make a function a friend of a class? (1 mark)**  
**A**

**34. What happens in External Fragmentation? (1 mark)**  
**B**

**35. Which of the following is NOT a core component of Apache Tomcat? (1 mark)**  
**D**

**36. What is the first step in a Servlet’s life cycle? (1 mark)**  
**D**

**37. What does the status code 500 indicate? (1 mark)**  
**C**

**38. a) List 6 properties of a file. (3 marks)**  
1. Name  
2. Size  
3. Type (extension)  
4. Creation date  
5. Last modified date  
6. Permissions (read/write/execute)  

**b) Give 4 examples of networking devices. (2 marks)**  
1. Router  
2. Switch  
3. Hub  
4. Modem  

**39. Which property ensures that data is delivered to the correct recipient? (1 mark)**  
**B**

### Page 5

**40. a) The ability to change the logical schema without altering external schemas is called... (2 marks)**  
**Answer**: Data Independence  

**40. b) The constraint used to link records between two tables is a... (2 marks)**  
**Answer**: Foreign Key  

**41. Write a Java program to demonstrate multilevel inheritance. Create three classes: Animal, Dog, and BabyDog, where Dog inherits from Animal and BabyDog inherits from Dog. Each class should have a method that prints a specific message (eat, bark, and weep respectively). Then, in a Test class, create an object of BabyDog and call all three methods. (5 marks)**  
```java
class Animal {
    void eat() {
        System.out.println("Animal is eating");
    }
}
class Dog extends Animal {
    void bark() {
        System.out.println("Dog is barking");
    }
}
class BabyDog extends Dog {
    void weep() {
        System.out.println("BabyDog is weeping");
    }
}
public class Test {
    public static void main(String[] args) {
        BabyDog babyDog = new BabyDog();
        babyDog.eat();   // From Animal
        babyDog.bark();  // From Dog
        babyDog.weep();  // From BabyDog
    }
}
```  
**Output**:  
```
Animal is eating
Dog is barking
BabyDog is weeping
```

**42. Authorization is the process of: (1 mark)**  
**C**

**43. Explain the role of each of the following protocols: (3 marks)**  
a) **DHCP (Dynamic Host Configuration Protocol)**: Automatically assigns IP addresses and network configuration (e.g., subnet mask, gateway) to devices on a network.  
b) **ARP (Address Resolution Protocol)**: Maps an IP address to a physical (MAC) address on a local network, enabling communication between devices.  
c) **ICMP (Internet Control Message Protocol)**: Facilitates error reporting and diagnostics in IP networks (e.g., ping, traceroute).  

**44. Choose the suitable word(s) to fill the following blanks: (5 marks)**  
a. **Process**  
b. **Long term scheduler**  
c. **PCB** (Process Control Block)  
d. **Dispatcher**  
e. **Short-term scheduler**  

**45. Assume that a database is connected to a Visual Basic form using the ADODC control. Provide the methods or actions required to: (5 marks)**  
a) **Add a new record**: `Adodc1.Recordset.AddNew`  
b) **Move to the next record**: `Adodc1.Recordset.MoveNext`  
c) **Move to the previous record**: `Adodc1.Recordset.MovePrevious`  
d) **Move to the first record**: `Adodc1.Recordset.MoveFirst`  
e) **Move to the last record**: `Adodc1.Recordset.MoveLast`  
f) **Delete the current record**: `Adodc1.Recordset.Delete`  

### Page 6

**46. Provide HTML and CSS code of the below form: (5 marks)**  
**Issue**: The OCR content for the form is corrupted (repetitive "\begin" tags), and no form description is provided.  
**Response**: Without a specific description of the form (e.g., fields, layout), I cannot provide accurate HTML and CSS code. A typical simple form with common fields (e.g., name, email, submit button) is assumed for illustrative purposes. If you provide the form's structure or fields, I can tailor the code accordingly.  

**Sample Code (Assumed Form)**:  
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Sample Form</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
        }
        .form-container {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        label {
            display: block;
            margin-bottom: 5px;
        }
        input[type="text"], input[type="email"] {
            width: 100%;
            padding: 8px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        input[type="submit"] {
            background-color: #4CAF50;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        input[type="submit"]:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <div class="form-container">
        <form>
            <label for="name">Name:</label>
            <input type="text" id="name" name="name" required>
            <label for="email">Email:</label>
            <input type="email" id="email" name="email" required>
            <input type="submit" value="Submit">
        </form>
    </div>
</body>
</html>
```  
**Note**: Please provide the specific form details (e.g., fields, labels, layout) for an accurate solution.

### Notes on Missing/Incomplete Questions:
- **Question 4**: Option D is corrupted, but upgrading RAM (C) is the most logical choice for video editing performance.
- **Question 46**: The form description is missing due to OCR errors. The provided code is a generic example. Please clarify the form's structure for a precise answer.
- **General**: Some questions (e.g., 27) were incomplete in the OCR but could be answered based on context. Others (e.g., 46) require additional details.
