# **Learning Outcome 2: Analyze Data Structures and Algorithms**

### 📘 Learning Hours: 10

---

## 📌 Objective

By the end of this section, learners will be able to:
- Understand time and space complexity.
- Calculate Big O notation for algorithms.
- Analyze the impact of data structures on algorithm efficiency.
- Select appropriate data structures for problems.

---

## 1. **Time Complexity**

### 1.1 Definition
Time complexity measures how an algorithm’s runtime grows with input size.

### 1.2 Example: Linear vs. Binary Search
- **Linear Search**: `O(n)` – checks each element.
- **Binary Search**: `O(log n)` – halves search space.

---

## 2. **Big O Notation**

### 2.1 Definition
Describes the upper bound of an algorithm’s complexity.

### 2.2 Example: Bubble Sort
```cpp
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++)
        for (int j = 0; j < n-i-1; j++)
            if (arr[j] > arr[j+1]) swap(arr[j], arr[j+1]);
}
```
- Time Complexity: `O(n²)`
- Space Complexity: `O(1)`

---

## 3. **Space Complexity**

### 3.1 Definition
Measures memory usage relative to input size.

### 3.2 Example: Recursive Function
```cpp
int sum(int n) {
    if (n <= 0) return 0;
    return n + sum(n-1);
}
```
- Space Complexity: `O(n)` due to call stack.

---

## 4. **Data Structures**

### 4.1 Definition
Organized formats for storing and managing data.

### 4.2 Types
| Type        | Examples                     |
|-------------|------------------------------|
| Linear      | Arrays, Linked Lists, Stacks |
| Non-Linear  | Trees, Graphs                |

---

## 5. **Data Structure Selection**

### 5.1 Definition
Choosing data structures based on problem requirements (e.g., access speed, data size).

### 5.2 Example
- **Fast Lookups**: Use hash tables (`O(1)`).
- **Ordered Data**: Use binary search trees (`O(log n)`).

---

## ✅ Summary Table
| Concept            | Description                        | Example                     |
|--------------------|------------------------------------|-----------------------------|
| Time Complexity    | Runtime growth with input size     | `O(n)` for linear search    |
| Big O Notation     | Upper bound of complexity          | `O(n²)` for bubble sort     |
| Space Complexity   | Memory usage                       | `O(n)` for recursive calls  |
| Data Structure     | Organized data storage             | Arrays, Trees               |

---

## 📚 Practice Exercises
1. Calculate the Big O notation for a nested loop iterating `n` times each.
2. Compare time complexity of linear search vs. binary search for 1000 elements.
3. Suggest a data structure for storing a phonebook with fast lookups.