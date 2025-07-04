# **Learning Outcome 4: Implement Integration**

### 📘 Learning Hours: 10

---

## 📌 Objective

By the end of this section, learners will be able to:
- Manage HTTP requests (methods, headers, status codes).
- Implement user authentication (token-based, two-factor).
- Integrate RESTful or GraphQL APIs and external services.
- Handle CORS, caching, and exception handling [cite: 174].

---

## 1. **Managing HTTP Requests**

### 1.1 Definition
Sending/receiving data via HTTP methods with headers and parameters [cite: 174].

### 1.2 Example: Fetching Properties
```jsx
import { useEffect } from 'react';
useEffect(() => {
  fetch('https://api.realestatepro.com/properties', {
    method: 'GET',
    headers: { 'Authorization': 'Bearer token123' },
  })
    .then(res => res.json())
    .then(data => console.log(data));
}, []);
```

---

## 2. **User Authentication**

### 2.1 Definition
Implementing secure login, token storage, and session management [cite: 174].

### 2.2 Example: Token-Based Authentication
```jsx
import AsyncStorage from '@react-native-async-storage/async-storage';
const login = async (credentials) => {
  const res = await fetch('https://api.realestatepro.com/login', {
    method: 'POST',
    body: JSON.stringify(credentials),
  });
  const { token } = await res.json();
  await AsyncStorage.setItem('token', token);
};
```

---

## 3. **Integrating APIs and External Services**

### 3.1 Definition
Connecting to RESTful or GraphQL APIs for data exchange [cite: 174].

### 3.2 Example: GraphQL Query
```javascript
import { gql, useQuery } from '@apollo/client';
const GET_PROPERTIES = gql`
  query {
    properties {
      name
      price
    }
  }
`;
```

### 3.3 API Types
| Type        | Description                              |
|-------------|------------------------------------------|
| RESTful     | Resource-based API with HTTP methods     |
| GraphQL     | Query-based API for flexible data fetch  |

---

## 4. **Exception Handling and CORS**

### 4.1 Definition
Managing errors and cross-origin issues during API calls [cite: 174].

### 4.2 Example: Error Handling
```jsx
const fetchData = async () => {
  try {
    const res = await fetch('https://api.realestatepro.com/properties');
    if (!res.ok) throw new Error('Network error');
    return await res.json();
  } catch (error) {
    console.error('Fetch error:', error);
  }
};
```

---

## ✅ Summary Table
| Concept               | Description                              | Example                        |
|-----------------------|------------------------------------------|--------------------------------|
| HTTP Requests         | Managing API calls                       | Fetching property list         |
| Authentication        | Secure login and session management      | Token storage with AsyncStorage|
| API Integration       | Connecting to APIs                       | GraphQL property query         |
| Exception Handling    | Managing errors and CORS                 | Try-catch for API fetch        |

---

## 📚 Practice Exercises
1. Implement a POST request to add a property with headers [cite: 174].
2. Create a login function with two-factor authentication using AsyncStorage [cite: 174].
3. Integrate a RESTful API to fetch property images [cite: 174].