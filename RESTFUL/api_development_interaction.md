# API Development and Interaction

### **Topic Overview**

This section introduces the fundamentals of working with RESTful APIs in JavaScript. It covers how to make HTTP requests using both modern and legacy approaches, explains secure authentication practices, and includes a comparison of HTTP protocol versions that affect API performance.

---

## Making RESTful API Calls in JavaScript

Interacting with RESTful APIs allows applications to communicate with servers to retrieve or modify data. JavaScript provides several ways to make HTTP requests, with `fetch()` being the modern standard.

### **1. `fetch()` (Modern Approach)**

* Built-in JavaScript method for making HTTP requests.
* Supports **Promises** and **async/await**, making it cleaner and easier to read.
* Widely supported in modern browsers.

**Example:**

```javascript
async function getUser(id) {
  const response = await fetch(`https://api.example.com/users/${id}`);
  const data = await response.json();
  return data;
}
```

### **2. `XMLHttpRequest` (Legacy Approach)**

* An older way to perform HTTP requests.
* More verbose and less readable than `fetch()`, but still fully supported.

**Example:**

```javascript
const xhr = new XMLHttpRequest();
xhr.open('GET', 'https://api.example.com/users/123');
xhr.onload = () => console.log(xhr.responseText);
xhr.send();
```

### **Incorrect Usage Examples**

* `post()` and `getRequest()` are not valid built-in JavaScript functions.
* Attempting to use these without defining them manually will result in errors.

### **Recommendation**

Use `fetch()` for new projects because it offers a more concise and modern API for handling HTTP communication.

---

## User Authentication in RESTful APIs

Authentication ensures that only authorized users can access specific resources. In RESTful APIs, authentication is usually handled via **token-based systems** and should be implemented securely.

### **Recommended Method: `POST /login`**

* Sends credentials (e.g., username and password) in the **request body**, not the URL.
* Ensures that sensitive data is **not exposed** in logs or browser history.

**Example:**

```javascript
fetch('https://api.example.com/login', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ username: 'user', password: 'pass' })
})
  .then(response => response.json())
  .then(data => console.log(data));
```

### **Methods to Avoid**

* `GET /login`: Insecure, exposes data in the URL.
* `PUT /auth`: Misused; intended for updating existing resources.
* `DELETE /auth`: Intended for removing resources, not logging in.

### **Best Practices for Authentication**

* Use **HTTPS** to encrypt all API traffic.
* Return a secure **authentication token** (e.g., JWT) upon successful login.
* Include the token in the `Authorization` header for all protected API requests:

  ```http
  Authorization: Bearer <token>
  ```

---

## Comparison of HTTP Versions

The HTTP protocol governs how clients and servers communicate over the web. Each version brings improvements that impact API efficiency and user experience.

| Feature                 | HTTP/1.1                          | HTTP/2                           | HTTP/3                                 |
| ----------------------- | --------------------------------- | -------------------------------- | -------------------------------------- |
| **Release Year**        | 1997                              | 2015                             | 2022                                   |
| **Transport Protocol**  | TCP                               | TCP                              | QUIC (UDP-based)                       |
| **Multiplexing**        | ❌ Only one request per connection | ✅ Multiple streams over one conn | ✅ Improved multiplexing                |
| **Header Compression**  | ❌ None                            | ✅ HPACK                          | ✅ QPACK                                |
| **Connection Handling** | Requires multiple TCP connections | Single TCP connection per server | Faster connection setup (0-RTT)        |
| **Performance**         | Slower with many assets           | Faster, but still limited by TCP | Fastest, optimized for mobile          |
| **Adoption**            | Widespread and legacy systems     | Widely adopted                   | Emerging, supported by modern browsers |

