# **Learning Outcome 3: Implement Linear Data Structures**

### 📘 Learning Hours: 40

---

## 📌 Objective

By the end of this section, learners will be able to:
- Implement arrays, linked lists, stacks, and queues in C++.
- Apply sorting and searching algorithms.
- Compare linear data structures for efficiency.

---

## 1. **Arrays**

### 1.1 Definition
Contiguous memory for elements of the same type.

### 1.2 Example: Vector
```cpp
#include <vector>
#include <iostream>
using namespace std;
int main() {
    vector<int> arr = {1, 2, 3};
    arr.push_back(4);
    for (int x : arr) cout << x << " ";
}
```
**Output**: `1 2 3 4`

---

## 2. **Sorting Algorithms**

### 2.1 Definition
Arrange elements in order (e.g., ascending).

### 2.2 Example: Insertion Sort
```cpp
void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```
- Time Complexity: `O(n²)`

---

## 3. **Searching Algorithms**

### 3.1 Definition
Find elements in a data structure.

### 3.2 Example: Binary Search
```cpp
int binarySearch(int arr[], int left, int right, int target) {
    if (right >= left) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        if (arr[mid] > target) return binarySearch(arr, left, mid - 1, target);
        return binarySearch(arr, mid + 1, right, target);
    }
    return -1;
}
```
- Time Complexity: `O(log n)`

---

## 4. **Linked Lists**

### 4.1 Definition
Nodes with data and a pointer to the next node.

### 4.2 Example: Singly Linked List
```cpp
struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};
Node* head = nullptr;
void insert(int val) {
    Node* newNode = new Node(val);
    newNode->next = head;
    head = newNode;
}
```

---

## 5. **Stacks**

### 5.1 Definition
LIFO (Last-In-First-Out) structure.

### 5.2 Example: Stack
```cpp
class Stack {
    int arr[100];
    int top = -1;
public:
    void push(int val) { arr[++top] = val; }
    int pop() { return arr[top--]; }
};
```

---

## 6. **Queues**

### 6.1 Definition
FIFO (First-In-First-Out) structure.

### 6.2 Example: Queue
```cpp
class Queue {
    int arr[100];
    int front = 0, rear = -1;
public:
    void enqueue(int val) { arr[++rear] = val; }
    int dequeue() { return arr[front++]; }
};
```

---

## ✅ Summary Table
| Structure    | Access | Insert | Delete | Example Use            |
|--------------|--------|--------|--------|------------------------|
| Array        | O(1)   | O(n)   | O(n)   | Static data storage    |
| Linked List  | O(n)   | O(1)   | O(1)   | Dynamic insertions     |
| Stack        | O(1)   | O(1)   | O(1)   | Undo functionality     |
| Queue        | O(1)   | O(1)   | O(1)   | Task scheduling        |

---

## 📚 Practice Exercises
1. Implement a function to reverse an array in C++.
2. Write a program to implement a doubly linked list with insertion and deletion.
3. Create a stack to check if parentheses in an expression are balanced.