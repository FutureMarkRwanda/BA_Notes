# **Learning Outcome 4: Implement Non-Linear Data Structures**

### 📘 Learning Hours: 25

---

## 📌 Objective

By the end of this section, learners will be able to:
- Implement trees, graphs, and maps in C++.
- Perform traversals and operations on non-linear structures.
- Apply non-linear structures to real-world problems.

---

## 1. **Trees**

### 1.1 Definition
Hierarchical structures with nodes connected as parent-child.

### 1.2 Example: Binary Search Tree
```cpp
struct Node {
    int data;
    Node *left, *right;
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};
Node* insert(Node* root, int val) {
    if (!root) return new Node(val);
    if (val < root->data) root->left = insert(root->left, val);
    else root->right = insert(root->right, val);
    return root;
}
```

---

## 2. **Graphs**

### 2.1 Definition
Nodes (vertices) connected by edges, representing relationships.

### 2.2 Example: Adjacency List
```cpp
#include <vector>
class Graph {
    int V;
    vector<vector<int>> adj;
public:
    Graph(int v) : V(v), adj(v) {}
    void addEdge(int u, int v) { adj[u].push_back(v); }
};
```

---

## 3. **Maps**

### 3.1 Definition
Key-value pair storage for efficient data association.

### 3.2 Example: `std::map`
```cpp
#include <map>
#include <iostream>
using namespace std;
int main() {
    map<string, int> scores;
    scores["Alice"] = 90;
    cout << scores["Alice"] << endl; // Outputs 90
}
```

---

## ✅ Summary Table
| Structure  | Access    | Insert    | Delete    | Example Use            |
|------------|-----------|-----------|-----------|------------------------|
| BST        | O(log n)  | O(log n)  | O(log n)  | Ordered data           |
| Graph      | O(V+E)    | O(1)      | O(E)      | Social networks        |
| Map        | O(log n)  | O(log n)  | O(log n)  | Dictionary lookup      |

---

## 📚 Practice Exercises
1. Implement a binary tree with pre-order traversal.
2. Write a program to represent a graph using an adjacency matrix.
3. Create a map to count the frequency of words in a sentence.