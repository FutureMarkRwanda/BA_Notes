# **Learning Outcome 5: Implement Hash Table and Handle Data Retrieval**

### 📘 Learning Hours: 10

---

## 📌 Objective

By the end of this section, learners will be able to:
- Design and implement hash tables in C++.
- Apply hash functions and collision resolution strategies.
- Optimize data retrieval using hash tables.

---

## 1. **Hash Tables**

### 1.1 Definition
Store key-value pairs using a hash function to map keys to indices.

### 1.2 Example: Chaining
```cpp
#include <list>
#include <vector>
class HashTable {
    int size;
    vector<list<int>> table;
    int hash(int key) { return key % size; }
public:
    HashTable(int s) : size(s), table(s) {}
    void insert(int key) { table[hash(key)].push_back(key); }
};
```

---

## 2. **Hash Functions**

### 2.1 Definition
Map keys to indices, ideally with uniform distribution.

### 2.2 Example
```cpp
int hashFunction(int key) {
    return key % 10; // Simple modulo hash
}
```

---

## 3. **Collision Resolution**

### 3.1 Definition
Handle cases where multiple keys map to the same index.

### 3.2 Techniques
| Technique       | Description                       |
|----------------|-----------------------------------|
| Chaining       | Use linked lists at each index    |
| Open Addressing| Probe for alternative slots       |

---

## ✅ Summary Table
| Concept            | Description                        | Example                     |
|--------------------|------------------------------------|-----------------------------|
| Hash Table         | Key-value storage                  | Chaining implementation     |
| Hash Function      | Maps keys to indices               | Modulo-based hash           |
| Collision Resolution | Handles key conflicts            | Linear probing, Chaining    |

---

## 📚 Practice Exercises
1. Implement a hash table with open addressing (linear probing).
2. Write a program to store student IDs in a hash table using chaining.
3. Compare the performance of `std::unordered_map` vs. a custom hash table.