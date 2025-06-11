# Unit 2: Complex Data Structures and Algorithms

## 2.1 Introduction to Data Structures
Data structures organize and store data efficiently to enable fast access and manipulation in programs.

- **Definition**: A data structure is a way to store and organize data in a computer for efficient use.
- **Types**:
  - **Primitive**: Basic types like `int`, `float`, `char`.
  - **Non-Primitive**: Complex structures like arrays, lists, stacks, queues, and trees.
- **Importance**:
  - Enhances program efficiency (speed and memory).
  - Supports solving complex problems like searching and sorting.
- **Example**: Storing student grades in an array for quick access.

## 2.2 Array of Elements in Data Structure
Arrays are collections of elements stored in contiguous memory, accessed by an index.

- **Characteristics**:
  - Fixed size (defined at declaration).
  - Elements are of the same data type.
  - Fast access using index (e.g., `arr[0]`).
- **Example (C++)**:
  ```cpp
  #include <iostream>
  int main() {
      int numbers[4] = {10, 20, 30, 40};
      std::cout << numbers[1] << std::endl; // Output: 20
      return 0;
  }
  ```
- **Advantages**:
  - Constant-time access (O(1)).
  - Simple implementation.
- **Disadvantages**:
  - Fixed size limits flexibility.
  - Inserting/deleting elements is slow (O(n)).

## 2.3 Abstract Data Types (ADTs)
ADTs define data and operations without specifying implementation details.

- **Definition**: A model for data structures that specifies behavior (operations) but not implementation.
- **Examples**:
  - **List ADT**: Operations like add, remove, get.
  - **Stack ADT**: Push, pop, top.
  - **Queue ADT**: Enqueue, dequeue, front.
- **Purpose**: Provides a high-level interface, allowing multiple implementations (e.g., List as array or linked list).
- **Example**: A stack ADT can be implemented using an array or linked list.

## 2.4 List
Lists are ordered collections of elements that can grow or shrink dynamically.

- **Types**:
  - **Array-Based List**: Uses an array (e.g., C++ `std::vector`).
  - **Linked List**: Nodes linked by pointers, each with data and a next pointer.
- **Operations**:
  - Push_back: Add an element to the end.
  - Insert: Add an element at a position.
  - Erase: Remove an element.
  - Access: Retrieve an element by index.
- **Example (C++ using `std::vector`)**:
  ```cpp
  #include <iostream>
  #include <vector>
  int main() {
      std::vector<int> my_list = {1, 2, 3};
      my_list.push_back(4); // Adds 4
      for (int x : my_list) {
          std::cout << x << " "; // Output: 1 2 3 4
      }
      return 0;
  }
  ```

## 2.5 Queue
A queue is a linear data structure following the First-In-First-Out (FIFO) principle.

- **Operations**:
  - **Enqueue**: Add an element to the rear.
  - **Dequeue**: Remove an element from the front.
  - **Front**: View the front element.
- **Types**:
  - **Simple Queue**: Basic FIFO.
  - **Circular Queue**: Rear connects to front.
  - **Priority Queue**: Elements dequeued by priority.
- **Example (C++ using `std::queue`)**:
  ```cpp
  #include <iostream>
  #include <queue>
  int main() {
      std::queue<int> q;
      q.push(1); // Enqueue
      q.push(2);
      std::cout << q.front() << std::endl; // Output: 1
      q.pop(); // Dequeue
      std::cout << q.front() << std::endl; // Output: 2
      return 0;
  }
  ```

## 2.6 Stack
A stack is a linear data structure following the Last-In-First-Out (LIFO) principle.

- **Operations**:
  - **Push**: Add an element to the top.
  - **Pop**: Remove the top element.
  - **Top**: View the top element.
- **Applications**: Undo operations, function call stack, expression evaluation.
- **Example (C++ using `std::stack`)**:
  ```cpp
  #include <iostream>
  #include <stack>
  int main() {
      std::stack<int> s;
      s.push(1); // Push
      s.push(2);
      std::cout << s.top() << std::endl; // Output: 2
      s.pop(); // Pop
      std::cout << s.top() << std::endl; // Output: 1
      return 0;
  }
  ```

## 2.7 Tree
A tree is a hierarchical data structure with nodes connected by edges, starting from a root.

- **Key Terms**:
  - **Root**: Topmost node.
  - **Leaf**: Node with no children.
  - **Height**: Longest path from root to leaf.
- **Types**:
  - **Binary Tree**: Each node has up to two children.
  - **Binary Search Tree (BST)**: Left child < parent < right child.
- **Applications**: File systems, decision trees, database indexing.
- **Example (C++)**:
  ```cpp
  #include <iostream>
  struct Node {
      int value;
      Node* left;
      Node* right;
      Node(int val) : value(val), left(nullptr), right(nullptr) {}
  };
  int main() {
      Node* root = new Node(1);
      root->left = new Node(2);
      root->right = new Node(3);
      std::cout << root->value << std::endl; // Output: 1
      return 0;
  }
  ```

## 2.8 Searching Using Complex Data Structures
Searching finds an element in a data structure.

- **Linear Search**:
  - Checks each element sequentially.
  - Time Complexity: O(n).
  - Example (C++):
    ```cpp
    #include <iostream>
    #include <vector>
    int linear_search(std::vector<int>& arr, int target) {
        for (int i = 0; i < arr.size(); i++) {
            if (arr[i] == target) return i;
        }
        return -1;
    }
    int main() {
        std::vector<int> arr = {10, 20, 30};
        std::cout << linear_search(arr, 20) << std::endl; // Output: 1
        return 0;
    }
    ```
- **Binary Search** (for sorted arrays or BST):
  - Divides search space in half each step.
  - Time Complexity: O(log n).
  - Example (C++):
    ```cpp
    #include <iostream>
    #include <vector>
    int binary_search(std::vector<int>& arr, int target) {
        int left = 0, right = arr.size() - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (arr[mid] == target) return mid;
            else if (arr[mid] < target) left = mid + 1;
            else right = mid - 1;
        }
        return -1;
    }
    int main() {
        std::vector<int> arr = {10, 20, 30, 40};
        std::cout << binary_search(arr, 30) << std::endl; // Output: 2
        return 0;
    }
    ```

## 2.9 Sorting Using Complex Data Structures
Sorting arranges elements in a specific order (e.g., ascending).

- **Bubble Sort**:
  - Repeatedly swaps adjacent elements if out of order.
  - Time Complexity: O(n²).
  - Example (C++):
    ```cpp
    #include <iostream>
    #include <vector>
    void bubble_sort(std::vector<int>& arr) {
        int n = arr.size();
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    std::swap(arr[j], arr[j + 1]);
                }
            }
        }
    }
    int main() {
        std::vector<int> arr = {64, 34, 25, 12};
        bubble_sort(arr);
        for (int x : arr) std::cout << x << " "; // Output: 12 25 34 64
        return 0;
    }
    ```
- **Merge Sort**:
  - Divides array into halves, sorts, and merges.
  - Time Complexity: O(n log n).
  - Example (C++):
    ```cpp
    #include <iostream>
    #include <vector>
    void merge(std::vector<int>& arr, int left, int mid, int right) {
        std::vector<int> temp(right - left + 1);
        int i = left, j = mid + 1, k = 0;
        while (i <= mid && j <= right) {
            if (arr[i] <= arr[j]) temp[k++] = arr[i++];
            else temp[k++] = arr[j++];
        }
        while (i <= mid) temp[k++] = arr[i++];
        while (j <= right) temp[k++] = arr[j++];
        for (i = 0; i < k; i++) arr[left + i] = temp[i];
    }
    void merge_sort(std::vector<int>& arr, int left, int right) {
        if (left < right) {
            int mid = left + (right - left) / 2;
            merge_sort(arr, left, mid);
            merge_sort(arr, mid + 1, right);
            merge(arr, left, mid, right);
        }
    }
    int main() {
        std::vector<int> arr = {64, 34, 25, 12};
        merge_sort(arr, 0, arr.size() - 1);
        for (int x : arr) std::cout << x << " "; // Output: 12 25 34 64
        return 0;
    }
    ```

## 2.10 Apply Algorithm to Solve Complex Mathematical Functions
Algorithms can solve mathematical problems efficiently using data structures.

- **Example Problem**: Calculate the Fibonacci sequence.
  - **Iterative Approach** (uses array):
    - Time Complexity: O(n).
    - Example (C++):
      ```cpp
      #include <iostream>
      #include <vector>
      int fibonacci(int n) {
          std::vector<int> fib(n + 1);
          fib[0] = 0; fib[1] = 1;
          for (int i = 2; i <= n; i++) {
              fib[i] = fib[i - 1] + fib[i - 2];
          }
          return fib[n];
      }
      int main() {
          std::cout << fibonacci(5) << std::endl; // Output: 5 (0, 1, 1, 2, 3, 5)
          return 0;
      }
      ```
  - **Recursive Approach** (uses stack implicitly):
    - Time Complexity: O(2^n) without optimization.
    - Example (C++):
      ```cpp
      #include <iostream>
      int fib_recursive(int n) {
          if (n <= 1) return n;
          return fib_recursive(n - 1) + fib_recursive(n - 2);
      }
      int main() {
          std::cout << fib_recursive(5) << std::endl; // Output: 5
          return 0;
      }
      ```
- **Using Trees**: Evaluate mathematical expressions using an expression tree.
  - Example: Expression `(2 + 3) * 4` can be represented as a tree and evaluated recursively.