# Additional Technology Questions and Answers

## Page 1

1. **What are the three primary goals of computer security?**  
   **Answer**: b) Confidentiality, Integrity, Availability  
   **Explanation**: These form the CIA triad, ensuring data is protected from unauthorized access (confidentiality), modified only by authorized users (integrity), and accessible when needed (availability).

2. **A virus typically goes through four phases. Which of the following is NOT one of them?**  
   **Answer**: d) Duplication phase  
   **Explanation**: The four phases of a virus are Dormant, Propagation, Triggering, and Execution. Duplication is not a standard phase.

3. **What does "integrity" in computer security imply?**  
   **Answer**: c) Data is modified only by authorized users  
   **Explanation**: Integrity ensures data remains accurate and is altered only by authorized entities, preventing unauthorized modifications.

4. **What is the function of "traffic analysis" in a cyberattack?**  
   **Answer**: a) Monitoring data for patterns of unauthorized access  
   **Explanation**: Traffic analysis involves observing network traffic patterns to identify unauthorized access or potential threats.

5. **Which type of attack involves sending repeated requests to overwhelm a system?**  
   **Answer**: c) Denial-of-Service  
   **Explanation**: A Denial-of-Service (DoS) attack floods a system with requests to disrupt its availability.

6. **Match each statement about symmetric and asymmetric cryptosystems (Column A) with the correct description (Column B).**  
   **Answer**:  
   1. Symmetric cryptosystems use a "symmetric key" → c) Uses the same secret key for both encrypting and decrypting data  
   2. Asymmetric cryptosystems require an "asymmetric key" → a) Involves two different keys: one for encryption (public) and one for decryption (private)  
   3. Symmetric cryptosystems → b) Generally exhibits faster encryption and decryption speeds  
   4. Asymmetric cryptosystems → d) Often slower in terms of encryption and decryption  

7. **Analyze the role of encryption in ensuring confidentiality. Provide an example.**  
   **Answer**: Encryption converts data into an unreadable format, ensuring only authorized users with the decryption key can access it, thus maintaining confidentiality. Example: AES encryption is used to secure sensitive data in HTTPS connections for secure web browsing.

8. **Evaluate the effectiveness of firewalls compared to antivirus software in securing networks.**  
   **Answer**:  
   - **Firewalls**: Monitor and filter network traffic based on rules, preventing unauthorized access. Effective for external threats but cannot detect malware already inside the system.  
   - **Antivirus Software**: Scans and removes malware from devices. Effective for internal threats but does not control network traffic.  
   - **Comparison**: Firewalls are proactive, blocking threats at the network level, while antivirus is reactive, addressing threats post-infection. Combining both provides comprehensive security.

## Page 2

9. **Propose a plan to mitigate the effects of a Denial-of-Service (DoS) attack.**  
   **Answer**:  
   - Deploy intrusion detection systems to identify unusual traffic patterns.  
   - Use load balancers to distribute traffic across multiple servers.  
   - Implement rate limiting to restrict excessive requests from a single source.  
   - Partner with a cloud-based DDoS protection service (e.g., Cloudflare).  
   - Maintain redundant servers to ensure availability during an attack.

10. **Which of these is a primary component of LAN architecture?**  
    **Answer**: b) NIC (Network Interface Card)  
    **Explanation**: NICs enable devices to connect to a LAN, unlike printers, monitors, or keyboards.

11. **What is the main role of the Physical layer in LAN architecture?**  
    **Answer**: b) Transmitting and receiving bits  
    **Explanation**: The Physical layer handles the transmission of raw bits over a physical medium.

12. **Determine whether each statement regarding the importance of the MAC protocol in LANs is True or False.**  
    **Answer**:  
    a) True - The MAC protocol prevents collisions by managing device transmission.  
    b) True - It controls access to the shared medium in the physical layer.  
    c) False - The MAC protocol does not assign IP addresses; that is handled by DHCP or manual configuration.

13. **Match the network characteristics in Column A with their corresponding definitions in Column B.**  
    **Answer**:  
    1. Range → a) The maximum distance over which a wireless signal can be reliably transmitted  
    2. Bandwidth → b) The amount of data that can be transmitted per unit of time over a wireless connection  

14. **Write the steps to configure a default gateway on a wireless router.**  
    **Answer**:  
    1. Log in to the router’s admin interface via a web browser (e.g., 192.168.0.1).  
    2. Navigate to the LAN or Network Settings section.  
    3. Locate the Default Gateway field.  
    4. Enter the IP address of the gateway (e.g., provided by ISP).  
    5. Save changes and restart the router if required.

15. **Demonstrate how to connect a device to a hidden SSID wireless network.**  
    **Answer**:  
    1. Access the device’s Wi-Fi settings.  
    2. Select “Add Network” or “Other Network.”  
    3. Manually enter the hidden SSID (network name).  
    4. Choose the security type (e.g., WPA2) and enter the password.  
    5. Connect to the network and verify connectivity.

16. **Analyze the following facts about the use of 2.4 GHz frequency for Wi-Fi networks and classify each as either an advantage or disadvantage.**  
    **Answer**:  
    1. Cheaper Devices – Advantage  
    2. Greater Range – Advantage  
    3. Lower Bandwidth – Disadvantage  
    4. Prone to Interference from Other Devices – Disadvantage  
    5. Congestion Due to More Connected Devices – Disadvantage  
    6. Universal Compatibility – Advantage  
    7. Limited Capacity for High-Speed Applications – Disadvantage  

## Page 3

17. **Susceptibility to Security Risks**  
    **Answer**: Disadvantage – 2.4 GHz networks are more vulnerable to attacks due to widespread use and older security protocols.

18. **Better Penetration Through Obstacles**  
    **Answer**: Advantage – 2.4 GHz signals penetrate walls and obstacles better than 5 GHz, improving coverage.

19. **Lower Power Consumption**  
    **Answer**: Advantage – 2.4 GHz devices typically consume less power, extending battery life.

20. **Compare wired Ethernet networks with wireless LANs.**  
    **Answer**:  
    - **Wired Ethernet**: Higher speed, lower latency, more secure, reliable; limited by cables, less mobility.  
    - **Wireless LANs**: Offers mobility, easy setup; susceptible to interference, lower security, variable performance.

21. **Critique the effectiveness of the OSI model for modern networking.**  
    **Answer**: The OSI model provides a structured framework for understanding networking but is theoretical, complex for practical implementation, and less relevant for modern protocols like TCP/IP, which combine layers.

22. **Assess the role of wireless access points in extending network coverage.**  
    **Answer**: Access points extend Wi-Fi coverage by acting as bridges between wired and wireless networks, improving connectivity in large areas but requiring proper placement and security configuration.

23. **Propose a method made of at least five measures to secure a wireless LAN against unauthorized access.**  
    **Answer**:  
    - Enable WPA3 encryption for strong security.  
    - Use a strong, unique password for the Wi-Fi network.  
    - Hide the SSID to reduce visibility.  
    - Implement MAC address filtering to allow only trusted devices.  
    - Regularly update router firmware to patch vulnerabilities.

24. **What type of cable is used to connect different devices, such as a computer to a switch?**  
    **Answer**: c) Straight-through cable  
    **Explanation**: Straight-through cables connect dissimilar devices (e.g., computer to switch), unlike crossover cables for similar devices.

25. **Which protocol is configured when assigning static IP addresses?**  
    **Answer**: b) IPv4  
    **Explanation**: Static IP addresses are assigned using the IPv4 protocol, defining device addresses in a network.

26. **Why is a switch preferred over a hub in a peer-to-peer (P2P) network with multiple computers?**  
    **Answer**: c) Switches forward data only to the intended recipient.  
    **Explanation**: Switches reduce collisions and improve efficiency by directing data to specific devices, unlike hubs, which broadcast to all.

27. **What role does the subnet mask play in IP configuration?**  
    **Answer**: The subnet mask divides an IP address into network and host portions, determining which devices are on the same network.

28. **The steps for making an Ethernet cable have been listed below in a disordered manner. Rearrange them in the correct order:**  
    **Answer**: b, e, c, a, d  
    1. Strip the cable jacket about 4cm from the end.  
    2. Untwist and align the wires in the T568A orientation on one end and T568B on the other.  
    3. Cut the wires straight and insert them into the RJ-45 connectors.  
    4. Crimp the connectors using an RJ-crimping tool.  
    5. Test the cable using a cable tester.

29. **Arrange the following statements to create a step-by-step process to verify network connectivity between two computers:**  
    **Answer**: e, d, a, c, b  
    1. Assign unique IP addresses to both computers.  
    2. Open the Command Prompt on one computer.  
    3. Type "ping" followed by IP addresses of another computer and press Enter.  
    4. Check the response for successful replies.  
    5. Troubleshoot any "Request timed out" messages by checking cables and configurations.

## Page 4

29. **(continued)**  
    **Answer**: As above (e, d, a, c, b).

30. **Compare static and dynamic IP addressing in terms of usability and management.**  
    **Answer**:  
    - **Static IP**: Fixed address, easier for servers; requires manual configuration, prone to conflicts.  
    - **Dynamic IP**: Automatically assigned via DHCP, simplifies management; less reliable for services requiring consistent addressing.

31. **Assess the significance of proper cable management in networking projects by answering by True or False for each of the following statements:**  
    **Answer**:  
    a) True – Reduces damage and disconnections.  
    b) True – Improves performance and reliability.  
    c) False – Enhances, not reduces, troubleshooting and upgrades.

32. **Propose a troubleshooting guide for resolving connectivity issues in a P2P network.**  
    **Answer**:  
    - Check physical connections (cables, ports).  
    - Verify IP configurations (static/dynamic, subnet mask).  
    - Ping devices to test connectivity.  
    - Ensure firewalls allow necessary traffic.  
    - Check for MAC address conflicts or filtering issues.

33. **What does SQL stand for?**  
    **Answer**: a) Structured Query Language  
    **Explanation**: SQL is used for managing and querying relational databases.

34. **Which of the following is a unary operation in relational algebra?**  
    **Answer**: c) Projection  
    **Explanation**: Projection selects specific columns, a unary operation, unlike binary operations like Union or Join.

35. **What symbol is used in relational algebra for selection?**  
    **Answer**: b) $\sigma$  
    **Explanation**: The $\sigma$ symbol denotes the selection operation, filtering rows based on a condition.

36. **Fill in the blank: In relational algebra, the SELECT operation is used to retrieve rows from a relation that satisfy a given condition, while the PROJECT operation is used to retrieve specific ______ from a relation.**  
    **Answer**: columns  
    **Explanation**: The PROJECT operation ($\Pi$) selects specific columns from a relation.

37. **What are the three main purposes of the PRIMARY KEY constraint?**  
    **Answer**:  
    - Ensures each row is uniquely identifiable.  
    - Prevents duplicate records.  
    - Enables efficient indexing and referencing by foreign keys.

38. **Why is the WHERE clause important in SQL queries?**  
    **Answer**: b) It filters rows based on a specified condition.  
    **Explanation**: The WHERE clause limits the rows returned by a query based on conditions, unlike sorting or grouping.

## Page 5

38. **(continued)**  
    **Answer**: b) It filters rows based on a specified condition.

39. **Determine whether the following statements about the conditions for performing a UNION operation are True or False:**  
    **Answer**:  
    a) True – Same number of columns required.  
    b) True – Corresponding columns must have compatible data types.  
    c) True – Column order does not matter as long as types match.  
    d) True – UNION removes duplicates; UNION ALL does not.  
    e) True – Attributes should be conceptually related, regardless of names.

40. **How does a NATURAL JOIN differ from other types of joins?**  
    **Answer**: c) It automatically matches columns with the same name and eliminates duplicates.  
    **Explanation**: NATURAL JOIN joins tables based on columns with identical names, unlike explicit joins using ON or USING.

41. **Correct any mistake in this SQL query to list all employees earning more than 50,000 from a table called Employee:**  
    **Answer**:  
    ```sql
    SELECT * FROM Employee WHERE Salary > 50000;
    ```  
    **Explanation**: The original query incorrectly placed WHERE before FROM and used < instead of >.

42. **Write the steps to add a new column 'Department' to an existing table 'Employee'.**  
    **Answer**:  
    1. Open the database management tool (e.g., SQL Server Management Studio).  
    2. Write the SQL query: `ALTER TABLE Employee ADD Department VARCHAR(50);`  
    3. Execute the query to add the column.  
    4. Verify the column addition using `DESCRIBE Employee;` or equivalent.

43. **Given the table "Employees", answer the questions provided below it:**  
    **Answer**: Assuming the Employees table has columns: EmployeeID, Name, Department, HireDate, Salary.  
    a) `SELECT * FROM Employees WHERE Department = 'IT';`  
    b) `SELECT SUM(Salary) FROM Employees WHERE Department = 'HR';`  
    c) `SELECT Name FROM Employees WHERE HireDate < '2020-01-01';`  

## Page 6

43. **(continued)**  
    d) `INSERT INTO Employees (EmployeeID, Name, Department, HireDate, Salary) VALUES (6, 'Sarth Let', 'Marketing', '2022-05-10', NULL);`  
    e) `DELETE FROM Employees WHERE Department = 'Finance';`  
    f) `SELECT Department, COUNT(*) AS EmployeeCount FROM Employees GROUP BY Department;`  
    g) `UPDATE Employees SET Salary = Salary * 1.10 WHERE Department = 'HR';`

44. **Match the following types of data integrity with their correct definitions:**  
    **Answer**:  
    1. Entity Integrity → c) Every table row must have a unique identifier (Primary Key)  
    2. Referential Integrity → b) Ensures foreign key values in a table correspond to primary keys in another table  
    3. Domain Integrity → a) Restricts data type, format, or range of values allowed in a column  
    4. User-Defined Integrity → d) Enforces specific business rules outside the above categories  

45. **Explain the three main categories of database threats, and what do they entail?**  
    **Answer**:  
    - **Unauthorized Access**: Gaining access to data without permission (e.g., hacking).  
    - **Data Corruption**: Intentional or accidental alteration of data (e.g., malware or hardware failure).  
    - **Denial of Service**: Disrupting database availability (e.g., overloading the server).

46. **Critique the advantages and limitations of using subqueries in SQL.**  
    **Answer**:  
    - **Advantages**: Allow complex queries within a single statement, improve readability for nested logic, and enable dynamic filtering.  
    - **Limitations**: Can reduce performance for large datasets, harder to debug, and may be less efficient than joins.

47. **Consider two tables below and create queries to answer each question:**  
    **Answer**: Assuming tables: Employees (EmpId, Name, EmpEmail, Salary, Age), Project (ProjectNo, ProjectName, Location, Duration, EmpId).  
    a) `SELECT Name, EmpEmail FROM Employees;`  
    b) `SELECT * FROM Employees WHERE Salary > 600000;`  
    c) `SELECT * FROM Employees WHERE EmpEmail LIKE '%@company.rw';`  
    d) `SELECT * FROM Employees ORDER BY Salary DESC;`  
    e) `SELECT COUNT(*) FROM Employees WHERE Age < 30;`  
    f) `SELECT e.Name, p.ProjectName, p.Location FROM Employees e JOIN Project p ON e.EmpId = p.EmpId;`  
    g) `SELECT * FROM Employees WHERE Salary = (SELECT MAX(Salary) FROM Employees);`  
    h) `SELECT e.Name FROM Employees e JOIN Project p ON e.EmpId = p.EmpId WHERE p.Location IN ('Kigali', 'Nyungwe');`  
    i) `SELECT Name, Salary FROM Employees WHERE Salary > (SELECT AVG(Salary) FROM Employees);`  
    j) `UPDATE Employees SET Salary = Salary * 1.05;`  
    k) `INSERT INTO Project (ProjectNo, ProjectName, Location, Duration, EmpId) VALUES (6, 'Rubavu Waterfront', 'Rubavu', 15, 6);`  
    l) `SELECT e.* FROM Employees e LEFT JOIN Project p ON e.EmpId = p.EmpId WHERE p.EmpId IS NULL;`

## Page 7

47. **(continued)**  
    **Answer**: As above.

48. **What is the starting index of an array in Visual Basic?**  
    **Answer**: c) 0  
    **Explanation**: Arrays in Visual Basic start at index 0 by default.

49. **What function is used to display a message box in Visual Basic?**  
    **Answer**: c) MsgBox  
    **Explanation**: MsgBox displays a message box for user interaction.

## Page 8

50. **What does the Len function in Visual Basic return?**  
    **Answer**: b) The length of a string including spaces  
    **Explanation**: Len returns the total number of characters in a string, including spaces.

51. **What is the significance of the ByVal and ByRef keywords for parameter passing in Visual Basic functions?**  
    **Answer**:  
    - **ByVal**: Passes a copy of the variable; changes do not affect the original.  
    - **ByRef**: Passes a reference to the variable; changes affect the original.

52. **How does the Mid function differ from the Left function?**  
    **Answer**: b) The Mid function starts at a specific position, while the Left function starts at the beginning.  
    **Explanation**: Mid extracts a substring from a specified position, while Left extracts from the start.

53. **Write a program to declare a one-dimensional array and initialize it with five names. Display the names in a list box.**  
    **Answer**:  
```vb
Private Sub Form_Load()
    Dim names(4) As String
    names(0) = "John"
    names(1) = "Jane"
    names(2) = "Jake"
    names(3) = "Alice"
    names(4) = "Bob"
    List1.Clear
    For i = 0 To 4
        List1.AddItem names(i)
    Next i
End Sub
```

54. **Demonstrate how to use the MsgBox function to confirm deletion of a record.**  
    **Answer**:  
```vb
Private Sub Command1_Click()
    Dim result As VbMsgBoxResult
    result = MsgBox("Are you sure you want to delete this record?", vbYesNo + vbQuestion, "Confirm Deletion")
    If result = vbYes Then
        MsgBox "Record deleted!", vbInformation
    Else
        MsgBox "Deletion cancelled.", vbInformation
    End If
End Sub
```

55. **Write a program to calculate the sum of all elements in a two-dimensional array of 10 elements.**  
    **Answer**:  
```vb
Private Sub Form_Load()
    Dim arr(1, 4) As Integer
    Dim sum As Integer
    ' Initialize array
    arr(0, 0) = 1: arr(0, 1) = 2: arr(0, 2) = 3: arr(0, 3) = 4: arr(0, 4) = 5
    arr(1, 0) = 6: arr(1, 1) = 7: arr(1, 2) = 8: arr(1, 3) = 9: arr(1, 4) = 10
    sum = 0
    For i = 0 To 1
        For j = 0 To 4
            sum = sum + arr(i, j)
        Next j
    Next i
    MsgBox "Sum of elements: " & sum
End Sub
```

56. **Analyze the advantages and disadvantages of using ByVal in function calls.**  
    **Answer**:  
    - **Advantages**: Protects original data from modification; safer for function calls.  
    - **Disadvantages**: Increases memory usage due to copying; slower for large data structures.

57. **Determine whether the following statements about the use of arrays for managing large datasets compared to individual variables are True or False:**  
    **Answer**:  
    a) True – Arrays simplify data management with a single name.  
    b) False – Individual variables are less memory-efficient for large datasets.  
    c) True – Arrays enable efficient iteration with loops.

58. **Compare the InputBox and MsgBox functions in terms of functionality.**  
    **Answer**:  
    - **InputBox**: Prompts user for input and returns a value; used for data collection.  
    - **MsgBox**: Displays messages or prompts for simple user interaction (e.g., Yes/No); does not return input.

59. **Assess the effectiveness of general procedures for reducing code duplication.**  
    **Answer**: General procedures (subroutines/functions) reduce code duplication by reusing logic, improving maintainability and readability. However, they may add slight overhead and require careful parameter management.

60. **Design a VB program to read marks of a student in five subjects using an array, compute their average, and display grades based on the average.**  
    **Answer**:  
```vb
Private Sub Form_Load()
    Text1.Text = "" ' Subject 1
    Text2.Text = "" ' Subject 2
    Text3.Text = "" ' Subject 3
    Text4.Text = "" ' Subject 4
    Text5.Text = "" ' Subject 5
    Command1.Caption = "Calculate Grade"
End Sub

Private Sub Command1_Click()
    Dim marks(4) As Single
    Dim sum As Single, avg As Single
    marks(0) = CSng(Text1.Text)
    marks(1) = CSng(Text2.Text)
    marks(2) = CSng(Text3.Text)
    marks(3) = CSng(Text4.Text)
    marks(4) = CSng(Text5.Text)
    sum = 0
    For i = 0 To 4
        sum = sum + marks(i)
    Next i
    avg = sum / 5
    Dim grade As String
    Select Case avg
        Case 80 To 100
            grade = "A"
        Case 70 To 79
            grade = "B"
        Case 60 To 69
            grade = "C"
        Case 50 To 59
            grade = "D"
        Case Else
            grade = "F"
    End Select
    MsgBox "Average: " & avg & vbCrLf & "Grade: " & grade
End Sub
```

## Page 9

60. **(continued)**  
    **Answer**: As above, with grades: 80-100 (A), 70-79 (B), 60-69 (C), 50-59 (D), Below 50 (F).

61. **Create a Visual Basic application that uses two functions Sum() and Average() respectively.**  
    **Answer**:  
```vb
Private Sub Form_Load()
    Command1.Caption = "Calculate Sum and Average"
End Sub

Private Function Sum(marks() As Single) As Single
    Dim total As Single
    total = 0
    For i = 0 To 14
        total = total + marks(i)
    Next i
    Sum = total
End Function

Private Function Average(total As Single) As Single
    Average = total / 15
End Function

Private Sub Command1_Click()
    Dim marks(14) As Single
    Dim i As Integer
    For i = 0 To 14
        marks(i) = CSng(InputBox("Enter mark for student " & (i + 1)))
    Next i
    Dim total As Single
    total = Sum(marks)
    Dim avg As Single
    avg = Average(total)
    MsgBox "Sum: " & total & vbCrLf & "Average: " & avg
End Sub
```

62. **By using a general procedure called Pattern(), create a Visual Basic application to print the following pattern using nested for loops.**  
    **Answer**: Assuming a simple pattern like a 5x5 star grid:  
```vb
Private Sub Pattern()
    Dim output As String
    For i = 1 To 5
        For j = 1 To 5
            output = output & "* "
        Next j
        output = output & vbCrLf
    Next i
    MsgBox output
End Sub

Private Sub Form_Load()
    Command1.Caption = "Show Pattern"
End Sub

Private Sub Command1_Click()
    Pattern
End Sub
```

63. **Which component connects a Visual Basic project to a physical database?**  
    **Answer**: d) Recordset  
    **Explanation**: A Recordset provides a logical interface to interact with database records.

64. **What is the purpose of a Recordset in Visual Basic?**  
    **Answer**: b) To provide logical representation of records  
    **Explanation**: Recordsets allow manipulation of database records in VB applications.

65. **What is the role of the Front End in a Visual Basic project?**  
    **Answer**: c) To provide the user interface for interacting with the application  
    **Explanation**: The front end handles user interaction, while the back end manages data.

66. **Determine whether the following statements about the key differences between DAO and ADO in Visual Basic are True or False:**  
    **Answer**:  
    a) True – DAO is optimized for Access; ADO supports multiple databases.  
    b) False – DAO performs better with Access; ADO is more versatile but slower for Access.  
    c) True – DAO is suited for desktop apps; ADO supports web/distributed apps.  
    d) True – ADO uses OLE DB for broader data source access.  
    e) False – ADO supports newer technologies compared to DAO.

## Page 10

66. **(continued)**  
    **Answer**: As above.

67. **Write a code snippet to add a new record to a database using ADO in Visual Basic.**  
    **Answer**:  
```vb
Private Sub AddRecord()
    Dim conn As New ADODB.Connection
    Dim rs As New ADODB.Recordset
    conn.Open "Provider=Microsoft.Jet.OLEDB.4.0;Data Source=C:\Database.mdb"
    rs.Open "SELECT * FROM Employees", conn, adOpenDynamic, adLockOptimistic
    rs.AddNew
    rs!Name = "John Doe"
    rs!Salary = 50000
    rs.Update
    rs.Close
    conn.Close
End Sub
```

68. **The steps for connecting a Visual Basic form to a database using ODBC are listed below in a disordered manner. Arrange them in the correct order:**  
    **Answer**: d, a, e, c, b  
    1. Open the Visual Basic project and add an ADO Data Control to the form.  
    2. Right-click the control and set the ConnectionString property to the ODBC source.  
    3. Set the RecordSource property to a table or query in the database.  
    4. Bind form controls (e.g., text boxes) to the ADO Data Control.  
    5. Run the form to interact with the database.

69. **Analyze the advantages and disadvantages of using ADO over DAO.**  
    **Answer**:  
    - **Advantages**: ADO supports multiple data sources, is more flexible, and suits web/distributed apps.  
    - **Disadvantages**: Slower for Access databases, more complex to configure than DAO.

70. **Determine whether the following statements about the importance of user interface principles in project success are True or False:**  
    **Answer**:  
    a) True – Improves user experience and intuitiveness.  
    b) False – Aesthetics alone are insufficient; functionality matters.  
    c) True – Reduces errors with clear feedback.  
    d) True – Enhances accessibility and reach.  
    e) True – Ignoring feedback leads to poor UX.

71. **What does the Process Control Block (PCB) NOT include?**  
    **Answer**: d) Heap allocation strategy  
    **Explanation**: PCB includes Process ID, registers, and program counter but not heap strategy.

72. **What is the role of the long-term scheduler?**  
    **Answer**: b) Loads processes from secondary storage to memory  
    **Explanation**: The long-term scheduler controls which processes enter the ready queue.

73. **Which condition is NOT required for a deadlock?**  
    **Answer**: c) Preemption  
    **Explanation**: Deadlocks require mutual exclusion, hold and wait, no preemption, and circular wait.

74. **Which statement about kernel-level threads is FALSE?**  
    **Answer**: c) They require a thread library for implementation.  
    **Explanation**: Kernel-level threads are managed by the OS, not a thread library.

75. **Provide steps to calculate average waiting time for a given set of processes using the FCFS scheduling algorithm. Include a brief example.**  
    **Answer**:  
    - **Steps**:  
      1. List processes with arrival and burst times.  
      2. Order processes by arrival time (FCFS).  
      3. Calculate completion time for each process.  
      4. Compute waiting time (Completion time - Arrival time - Burst time).  
      5. Calculate average waiting time (Sum of waiting times / Number of processes).  
    - **Example**: Processes P1 (Arrival: 0, Burst: 5), P2 (Arrival: 1, Burst: 3).  
      - P1 completes at 5, waiting time = 5 - 0 - 5 = 0.  
      - P2 completes at 8, waiting time = 8 - 1 - 3 = 4.  
      - Average waiting time = (0 + 4) / 2 = 2 ms.

76. **Compare the advantages and disadvantages of user-level threads versus kernel-level threads.**  
    **Answer**:  
    - **User-Level Threads**:  
      - **Advantages**: Faster to create/switch, no OS overhead, portable.  
      - **Disadvantages**: Blocked thread blocks entire process, no multiprocessing.  
    - **Kernel-Level Threads**:  
      - **Advantages**: Supports multiprocessing, better scheduling.  
      - **Disadvantages**: Slower due to OS involvement, less portable.

77. **Discuss the role of aging in addressing starvation in priority scheduling. Provide an example.**  
    **Answer**: Aging increases the priority of low-priority processes over time to prevent starvation. Example: A low-priority process waiting for 10 time units gains priority incrementally, ensuring it eventually runs.

78. **Assess how deadlocks affect process management. Propose strategies to handle deadlocks.**  
    **Answer**: Deadlocks halt processes, reducing system efficiency. **Strategies**:  
    - Prevent deadlocks by ensuring no circular wait (resource ordering).  
    - Detect and recover by terminating processes or rolling back.  
    - Avoid deadlocks using banker’s algorithm.  

79. **Given the following processes with their burst time, arrival time, and priority:**  
    **Answer**:  
    a) **Gantt Charts**:  
    - **Preemptive SJF**:  
      ```
      | P1 | P3 | P4 | P2 | P5 | P6 | P1 |
      0    2    3    4    7    9   11   14
      ```  
      - **Non-Preemptive SJF**:  
      ```
      | P1 | P2 | P3 | P4 | P5 | P6 |
      0    8   12   14   15   18   20
      ```  
    b) **Average Waiting Time**:  
      - Preemptive SJF: (0 + (7-1-4) + (2-2-2) + (3-3-1) + (9-4-3) + (11-5-2)) / 6 = 2 ms  
      - Non-Preemptive SJF: (0 + (8-1-4) + (12-2-2) + (14-3-1) + (15-4-3) + (18-5-2)) / 6 = 5 ms  
    c) **Average Turnaround Time**:  
      - Preemptive SJF: (14-0 + 7-1 + 3-2 + 4-3 + 9-4 + 11-5) / 6 = 5.33 ms  
      - Non-Preemptive SJF: (8-0 + 12-1 + 14-2 + 15-3 + 18-4 + 20-5) / 6 = 11.33 ms  

## Page 11

79. **(continued)**  
    **Answer**: As above.

80. **Which of the following is a property of a file?**  
    **Answer**: c) Identifier  
    **Explanation**: Files have identifiers (names), unlike processor type or memory bus width.

81. **What is the primary difference between text files and binary files?**  
    **Answer**: b) Text files are ASCII/Unicode-based, binary files store custom data  
    **Explanation**: Text files store readable characters; binary files store data in a non-readable format.

82. **How does NTFS ensure security for files and folders?**  
    **Answer**: b) Through advanced encryption and permissions  
    **Explanation**: NTFS uses access control lists and encryption (EFS) for security.

83. **In Windows, how is a hidden attribute assigned to a file?**  
    **Answer**: b) By right-clicking and selecting properties  
    **Explanation**: In Windows, the hidden attribute is set via the file’s properties dialog.

84. **Illustrate with examples the hierarchical structure of a file system.**  
    **Answer**: A hierarchical file system organizes files in a tree structure. Example:  
    - Root (C:\)  
      - Folder: Users  
        - Folder: John  
          - File: document.txt  
      - Folder: Program Files  
        - File: app.exe  

85. **Fill in the blanks to compare and contrast the three file allocation methods:**  
    **Answer**:  
    a) Contiguous allocation stores files in **consecutive** blocks of storage, which can lead to issues like fragmentation but allows fast access speed.  
    b) Linked allocation uses **pointers** to point to the next block, allowing dynamic file size adjustment, but can suffer from slower access.  
    c) Indexed allocation stores **pointers** to data blocks in a special index table, providing **faster** access but requiring more storage for the index.

86. **Determine whether the following statements about the importance of proper file and allocation strategies in operating systems are True or False:**  
    **Answer**:  
    a) False – Proper allocation reduces fragmentation and optimizes space.  
    b) True – Improper allocation slows data retrieval.  
    c) True – Efficient allocation improves performance.  
    d) False – Allocation is crucial for all systems.  
    e) False – Good allocation enhances reliability and recovery.

87. **Propose a plan for improving file security in a shared network environment.**  
    **Answer**:  
    - Use strong encryption for sensitive files.  
    - Implement role-based access control (RBAC).  
    - Enable audit logging to track file access.  
    - Regularly update file permissions.  
    - Use secure file transfer protocols (e.g., SFTP).

88. **Which of the following is an example of non-volatile memory?**  
    **Answer**: c) ROM  
    **Explanation**: ROM retains data without power, unlike RAM, cache, or buffer memory.

89. **Which of the following describes internal fragmentation?**  
    **Answer**: b) Wastage of memory inside an allocated block  
    **Explanation**: Internal fragmentation occurs when allocated memory is larger than needed.

90. **Why is cache memory used between the CPU and main memory?**  
    **Answer**: a) To reduce access time for frequently used data  
    **Explanation**: Cache stores frequently accessed data to speed up CPU operations.

91. **What happens during demand paging?**  
    **Answer**: b) Only required pages are loaded into memory  
    **Explanation**: Demand paging loads pages as needed, improving memory efficiency.

## Page 12

92. **What is the primary role of the MMU in memory management?**  
    **Answer**: b) To convert logical addresses to physical addresses  
    **Explanation**: The Memory Management Unit (MMU) maps virtual addresses to physical memory.

93. **Given a process of size 3MB and three available partitions of sizes 2MB, 4MB, and 5MB, which partition would you allocate using the best-fit algorithm? Explain.**  
    **Answer**: 4MB partition. Best-fit allocates the smallest partition that can accommodate the process (3MB fits in 4MB, not 2MB; 5MB is larger than needed).

94. **Explain how compaction can resolve external fragmentation.**  
    **Answer**: Compaction moves allocated memory blocks to one end of memory, consolidating free space to eliminate external fragmentation.

95. **Determine whether the following statements about fixed and dynamic partitioning techniques in terms of memory utilization are True or False:**  
    **Answer**:  
    a) False – Fixed partitioning causes internal fragmentation.  
    b) True – Dynamic partitioning reduces internal but causes external fragmentation.  
    c) False – Fixed partitioning is less efficient due to fragmentation.  
    d) True – Dynamic partitioning is complex and causes fragmentation.  
    e) True – Fixed partitioning wastes memory if processes don’t fit.

96. **Assess the role of virtual memory in enhancing multitasking.**  
    **Answer**: Virtual memory allows multiple processes to run simultaneously by providing each process its own address space, improving resource utilization but increasing overhead.

97. **Propose a strategy to minimize both internal and external fragmentation in a memory management system.**  
    **Answer**:  
    - Use dynamic partitioning to reduce internal fragmentation.  
    - Implement compaction to address external fragmentation.  
    - Use paging to allocate fixed-size blocks.  
    - Employ memory pools for small allocations.  
    - Monitor and optimize allocation algorithms.

98. **Which Java collection allows duplicate elements and maintains insertion order?**  
    **Answer**: c) ArrayList  
    **Explanation**: ArrayList allows duplicates and preserves insertion order.

99. **What is the main difference between HashSet and LinkedHashSet?**  
    **Answer**: b) LinkedHashSet maintains insertion order; HashSet does not.  
    **Explanation**: LinkedHashSet uses a linked list to maintain order, unlike HashSet.

100. **Why is ArrayList preferred over arrays in Java?**  
     **Answer**: b) ArrayLists resize dynamically and provide utility methods for manipulation.  
     **Explanation**: ArrayLists offer flexibility and methods like add/remove, unlike fixed-size arrays.

## Page 13

100. **(continued)**  
     **Answer**: b) ArrayLists resize dynamically and provide utility methods for manipulation.

101. **Which Java Collection is best suited for maintaining a sorted order of elements?**  
     **Answer**: c) TreeSet  
     **Explanation**: TreeSet automatically sorts elements using natural ordering or a comparator.

102. **Write a Java code snippet to demonstrate adding and retrieving elements from an ArrayList.**  
     **Answer**:  
```java
import java.util.ArrayList;

public class ArrayListDemo {
 public static void main(String[] args) {
     ArrayList<String> list = new ArrayList<>();
     list.add("Apple");
     list.add("Banana");
     list.add("Orange");
     for (String item : list) {
         System.out.println(item);
     }
 }
}
```

103. **Demonstrate the usage of the poll() and peek() methods in a Java Queue.**  
     **Answer**:  
```java
import java.util.LinkedList;
import java.util.Queue;

public class QueueDemo {
 public static void main(String[] args) {
     Queue<String> queue = new LinkedList<>();
     queue.add("John");
     queue.add("Jane");
     queue.add("Jake");
     System.out.println("Peek: " + queue.peek()); // View first element
     System.out.println("Poll: " + queue.poll()); // Remove and return first element
     System.out.println("After poll, peek: " + queue.peek());
 }
}
```

104. **Evaluate the pros and cons of using TreeSet over HashSet.**  
     **Answer**:  
     - **Pros**: TreeSet maintains sorted order, supports range queries.  
     - **Cons**: Slower performance (O(log n) vs. O(1) for HashSet), higher memory usage.

105. **Determine whether the following statements about the PriorityQueue class in Java are True or False:**  
     **Answer**:  
     a) False – PriorityQueue is not thread-safe.  
     b) False – A comparator is needed for custom ordering.  
     c) True – Uses natural ordering or a comparator.  
     d) False – Allows duplicates.  
     e) True – Constant-time access, linear-time removal.

106. **Design a program to demonstrate the use of HashSet for filtering duplicate elements.**  
     **Answer**:  
```java
import java.util.HashSet;

public class HashSetDemo {
 public static void main(String[] args) {
     HashSet<String> set = new HashSet<>();
     set.add("Apple");
     set.add("Banana");
     set.add("Apple");
     set.add("Orange");
     System.out.println("Unique elements: " + set);
 }
}
```

107. **What is the primary purpose of Apache Tomcat?**  
     **Answer**: b) To serve Java applications  
     **Explanation**: Tomcat is a servlet container for running Java web applications.

108. **What does the status code 404 indicate in an HTTP response?**  
     **Answer**: c) Resource not found  
     **Explanation**: 404 indicates the requested resource is unavailable.

109. **Why is Catalina important in the Tomcat architecture?**  
     **Answer**: b) It acts as the servlet container  
     **Explanation**: Catalina processes servlet and JSP requests in Tomcat.

110. **What is the significance of the JSP engine (Jasper) in Tomcat?**  
     **Answer**: c) It converts JSP files into servlets  
     **Explanation**: Jasper parses and compiles JSP files into executable servlets.

## Page 14

110. **(continued)**  
     **Answer**: c) It converts JSP files into servlets.

111. **Write a code snippet to configure a new user in the Tomcat-users.xml file.**  
     **Answer**:  
```xml
<user username="admin" password="admin123" roles="manager-gui,admin-gui"/>
```

112. **The steps for starting a newly installed Tomcat server are listed below in a disordered manner. Arrange them in the correct order:**  
     **Answer**: d, a, c, e, b  
     1. Start the Tomcat server from the Start menu shortcuts.  
     2. Open a web browser.  
     3. Navigate to http://localhost:8080.  
     4. Verify the appearance of the Tomcat homepage.  
     5. Troubleshoot using logs if the page does not load.

113. **Determine whether the following statements about the differences between static and dynamic web pages are True or False:**  
     **Answer**:  
     a) True – Static pages are fixed; dynamic pages change with input.  
     b) False – Dynamic pages require server-side scripting.  
     c) True – Dynamic pages are interactive and database-driven.  
     d) True – Static pages load faster.  
     e) False – Dynamic pages suit frequently changing content.

114. **Assess the significance of HTTP status codes in debugging web applications.**  
     **Answer**: HTTP status codes (e.g., 404, 500) identify issues like missing resources or server errors, guiding developers to pinpoint and resolve problems efficiently.

115. **Design a dynamic web page using JSP that displays user-submitted data namely name and age.**  
     **Answer**:  
```
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
 <title>User Data</title>
</head>
<body>
 <h2>Enter User Data</h2>
 <form method="post">
     Name: <input type="text" name="name"><br>
     Age: <input type="number" name="age"><br>
     <input type="submit" value="Submit">
 </form>
 <% 
     String name = request.getParameter("name");
     String age = request.getParameter("age");
     if (name != null && age != null) {
         out.println("<h3>Submitted Data:</h3>");
         out.println("Name: " + name + "<br>");
         out.println("Age: " + age);
     }
 %>
</body>
</html>
```

116. **What is a pixel in computer graphics?**  
     **Answer**: c) The smallest graphical unit on a screen  
     **Explanation**: A pixel is the smallest addressable element in a display.

117. **Which of these is an example of a raster file format?**  
     **Answer**: a) TIFF  
     **Explanation**: TIFF is raster-based, unlike vector formats like SVG or EPS.

118. **Why are vector graphics preferred for scalable images?**  
     **Answer**: c) They do not lose quality when resized.  
     **Explanation**: Vector graphics use mathematical formulas, ensuring scalability without pixelation.

## Page 15

119. **Fill in the blanks to explain the difference between 2D and 3D graphics:**  
    **Answer**:  
    a) 2D graphics represent objects using **two** dimensions, typically width and height.  
    b) 3D graphics represent objects using **three** dimensions, including width, height, and **depth**.  
    c) 2D graphics are commonly used in **2D games or UI design** applications, while 3D graphics are used in simulations and modeling.

120. **Write a formula to calculate the size of an uncompressed image file.**  
    **Answer**: Size (bytes) = Width × Height × Bit Depth / 8  
    **Explanation**: Multiply dimensions by bit depth (bits per pixel) and divide by 8 to convert to bytes.

121. **Compare the features of TIFF and JPEG file formats.**  
    **Answer**:  
    - **TIFF**: Lossless, high quality, larger file size, supports layers, used in professional imaging.  
    - **JPEG**: Lossy compression, smaller file size, suitable for web, but degrades with repeated edits.

122. **Determine whether the following statements about the role of image compression in optimizing web performance are True or False:**  
    **Answer**:  
    a) True – Compression reduces file size, speeding up load times.  
    b) False – Compression reduces bandwidth usage.  
    c) True – Over-compression degrades quality.  
    d) True – Balances quality and performance.  
    e) False – Compression remains relevant for performance.

123. **Propose a workflow for processing and compressing images for web use.**  
    **Answer**:  
    - Resize images to web-appropriate dimensions.  
    - Choose a format (e.g., JPEG for photos, PNG for graphics).  
    - Compress using tools like Photoshop or TinyPNG.  
    - Optimize metadata and remove unnecessary data.  
    - Test image quality and load time on a website.

124. **What does multimedia primarily combine?**  
    **Answer**: b) Text, audio, images, animations, and video  
    **Explanation**: Multimedia integrates multiple media types for rich content.

125. **What does VFX stand for in multimedia applications?**  
    **Answer**: b) Visual Effects  
    **Explanation**: VFX refers to visual effects used in multimedia like films.

126. **Why is multimedia important in education?**  
    **Answer**: a) It makes learning more engaging and interactive.  
    **Explanation**: Multimedia enhances understanding through diverse, interactive content.

## Page 16

126. **(continued)**  
    **Answer**: a) It makes learning more engaging and interactive.

127. **The steps to create a hyperlink in a PowerPoint presentation are listed below in a disordered manner. Arrange them in the correct order:**  
    **Answer**: d, e, b, c, a  
    1. Select the text or image to hyperlink.  
    2. Right-click and choose "Hyperlink" or go to Insert > Hyperlink.  
    3. In the dialog box, choose the target (webpage, file, or slide).  
    4. Enter the link or select the file/slide.  
    5. Click "Ok" to apply the hyperlink.

128. **Fill in the blanks to compare the features of AVI and MP4 video formats:**  
    **Answer**:  
    a) AVI offers **high** video quality but results in **larger** file sizes compared to MP4.  
    b) MP4 is more suitable for **web streaming** due to its efficient compression and smaller file sizes.  
    c) AVI supports fewer **features** compared to MP4, such as subtitles and metadata.  
    d) MP4 is widely supported across **modern** devices and platforms.

129. **Assess the significance of interactive multimedia in medical training.**  
    **Answer**: Interactive multimedia enhances medical training by providing simulations, 3D visualizations, and interactive case studies, improving skill retention but requiring high development costs.

130. **Propose a workflow for enhancing an audio file to remove noise and enhance quality.**  
    **Answer**:  
    - Import audio into software (e.g., Audacity).  
    - Apply noise reduction to remove background noise.  
    - Use equalization to balance frequencies.  
    - Normalize audio to adjust volume levels.  
    - Export in a high-quality format (e.g., WAV or MP3).

131. **What does the fstream class provide in C++?**  
    **Answer**: c) Both reading and writing functionalities  
    **Explanation**: fstream supports both input and output operations for files.

132. **What is the primary purpose of file handling in C++?**  
    **Answer**: b) To store data permanently  
    **Explanation**: File handling enables persistent data storage.

133. **Why is the close() function essential in file handling?**  
    **Answer**: a) It prevents memory leaks by releasing resources used by the file.  
    **Explanation**: close() ensures resources are freed and data is saved.

## Page 17

134. **Determine whether the following statements about the role of the ios::app mode when opening a file are True or False:**  
    **Answer**:  
    a) True – ios::app adds data to the end of the file.  
    b) False – ios::app does not overwrite; it appends.  
    c) False – The file pointer is positioned at the end.

135. **Write a program to append data to an existing text file called example in C++.**  
    **Answer**:  
```
#include <fstream>
#include <iostream>
using namespace std;
    
int main() {
    fstream file;
    file.open("example.txt", ios::app);
    if (file.is_open()) {
        file << "Appended text\n";
        file.close();
        cout << "Data appended successfully" << endl;
    } else {
        cout << "Error opening file" << endl;
    }
    return 0;
}

```

136. **Compare the functionalities of ifstream and ofstream classes in C++.**  
    **Answer**:  
    - **ifstream**: Used for reading files; supports input operations.  
    - **ofstream**: Used for writing files; supports output operations.  
    - **fstream**: Combines both functionalities but is less specific.

137. **Assess the importance of file extensions in determining file types.**  
    **Answer**: File extensions indicate file format and associated applications, aiding in proper handling but can be misleading if renamed.

138. **Design a program to count the number of words in a text file.**  
    **Answer**:  
```
#include <fstream>
#include <iostream>
#include <string>
using namespace std;

int main() {
    ifstream file("example.txt");
    string word;
    int count = 0;
    if (file.is_open()) {
        while (file >> word) {
            count++;
        }
        file.close();
        cout << "Number of words: " << count << endl;
    } else {
        cout << "Error opening file" << endl;
    }
    return 0;
}
```