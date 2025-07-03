# **Learning Outcome 6: Apply Recursion for Solving Complex Problems Using C++**

### 📘 Learning Hours: 15

---

## 📌 Objective

By the end of this section, learners will be able to:
- Write recursive functions with proper base cases.
- Apply recursion to manipulate data structures.
- Optimize recursive algorithms using memoization.

---

## 1. **Recursion**

### 1.1 Definition
A function that calls itself to solve smaller instances of a problem.

### 1.2 Example: Fibonacci
```cpp
int fibonacci(int n) {
    if (n <= 1) return n; // Base case
    return fibonacci(n-1) + fibonacci(n-2); // Recursive call
}
```

---

## 2. **Base Cases**

### 2.1 Definition
Conditions that terminate recursion.

### 2.2 Example: Sum
```cpp
int sum(int n) {
    if (n <= 0) return 0; // Base case
    return n + sum(n-1); // Recursive call
}
```

---

## 3. **Recursive Data Structure Manipulation**

### 3.1 Definition
Using recursion to traverse or modify structures like trees.

### 3.2 Example: Tree Traversal
```cpp
struct Node {
    int data;
    Node *left, *right;
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};
void inorder(Node* root) {
    if (!root) return; // Base case
    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}
```

---

## ✅ Summary Table
| Concept            | Description                        | Example                     |
|--------------------|------------------------------------|-----------------------------|
| Recursion          | Self-calling function              | Fibonacci calculation       |
| Base Case          | Terminates recursion               | `n <= 1` in Fibonacci       |
| Memoization        | Caches results for efficiency      | Optimized Fibonacci         |

---

## 📚 Practice Exercises
1. Write a recursive function to reverse a string.
2. Implement a recursive algorithm for post-order tree traversal.
3. Optimize the Fibonacci function using memoization.