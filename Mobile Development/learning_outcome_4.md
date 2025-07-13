# Learning Outcome 4: Implement Integration

This section addresses key integration concepts essential for developing secure, connected mobile applications using React Native. It covers HTTP communication, authentication strategies, and API/external service integration. These skills are critical to building a scalable, secure application such as **RealEstatePro**, where multiple user roles interact with backend services.

---

## 1. HTTP Requests

### HTTP Methods: GET, POST, PUT, DELETE

**Purpose:**
HTTP methods define the type of operation performed on a server resource within a RESTful API.

| Method | Use Case Example                                        |
| ------ | ------------------------------------------------------- |
| GET    | Retrieve resources (e.g., fetch property listings)      |
| POST   | Create new resources (e.g., add a property)             |
| PUT    | Update existing resources (e.g., edit property info)    |
| DELETE | Remove resources (e.g., delete a property - admin only) |

**Implementation in React Native:**
Use `fetch` or `axios`:

```js
axios.get('https://api.realestatepro.com/properties');
```

---

### Headers, Body, Parameters

* **Headers**: Carry metadata such as content type and authorization tokens.

  ```js
  { 'Content-Type': 'application/json', 'Authorization': 'Bearer <token>' }
  ```
* **Body**: Used in POST/PUT to send data as JSON payloads.

  ```json
  { "name": "Apartment", "price": 200000 }
  ```
* **Parameters**:

  * *Query*: `/properties?type=rent`
  * *Path*: `/properties/123`

**RealEstatePro Example:**

* Use POST with headers and a body to create a property.
* Use query parameters to filter property listings.

---

### Caching, Rate Limiting, Throttling, HTTPS

* **Caching**: Store frequent API responses using `@react-native-async-storage/async-storage` to reduce calls and support offline access.
* **Rate Limiting**: Server-side constraint (e.g., 100 requests/hour). Detect HTTP 429 errors and inform users.
* **Throttling**: Implement debounce logic client-side to prevent excessive requests (e.g., during search).
* **HTTPS**: Use secure endpoints (HTTPS) and valid SSL certificates to protect data in transit.

**RealEstatePro Application:**

* Cache property lists locally.
* Handle 429 errors for client-side search.
* Ensure all API endpoints use `https://`.

---

## 2. User Authentication

### Identification, Verification, Authorization

| Concept        | Description                                        |
| -------------- | -------------------------------------------------- |
| Identification | User provides identity (e.g., email)               |
| Verification   | Credentials (e.g., password) are validated         |
| Authorization  | User roles determine access (admin, agent, client) |

**RealEstatePro Example:**

* Identify user at login.
* Verify credentials using the backend.
* Authorize access (e.g., agents cannot delete, clients can only view).

---

### Token-Based Authentication (JWT)

**Process:**

1. User logs in → server returns a **JWT**.
2. JWT is stored in **AsyncStorage**.
3. All protected requests include the token in the header:

   ```js
   Authorization: Bearer <token>
   ```

**Implementation in React Native:**

```js
await AsyncStorage.setItem('token', jwtToken);
```

**RealEstatePro Application:**

* Authenticate users using JWT.
* Send the token in every request to protected endpoints.

---

### 2FA, Session Management, AsyncStorage

* **2FA (Two-Factor Authentication)**: Add an additional verification layer (e.g., Firebase or Auth0).
* **Session Management**:

  * Use access tokens with expiration.
  * Optionally use refresh tokens.
  * Clear session data on logout.
* **AsyncStorage**:

  * Store user tokens and roles securely.

  ```js
  AsyncStorage.setItem('user', JSON.stringify({ id: 1, role: 'agent' }));
  ```

**RealEstatePro Example:**

* Use Firebase to enable 2FA for admin logins.
* Store user data and token in AsyncStorage.
* Clear session on logout using `AsyncStorage.removeItem()`.

---

## 3. APIs and External Services

### REST vs GraphQL

| Feature     | REST                                     | GraphQL                            |
| ----------- | ---------------------------------------- | ---------------------------------- |
| Endpoint    | Multiple (e.g., `/users`, `/properties`) | Single endpoint (`/graphql`)       |
| Query Style | Defined by server                        | Client-defined queries             |
| Use Case    | Simple CRUD operations                   | Complex nested or filtered queries |

**RealEstatePro Application:**

* Use REST for standard CRUD (e.g., create/update property).
* Use GraphQL to fetch nested data (e.g., properties with owner details).

---

### Fetching and Parsing Data

* **Fetching**:

  ```js
  const response = await axios.get('/properties');
  ```
* **Parsing**:

  ```js
  const properties = response.data.map(item => ({ id: item.id, name: item.name }));
  ```

**RealEstatePro Example:**

* Fetch data for a `FlatList` component.
* Normalize API responses for state storage.

---

### Handling CORS

**Issue:**
CORS errors occur when a frontend app makes a request to a backend on a different origin (e.g., mobile app calling a remote API).

**Solution:**

* Server must send headers like:

  ```http
  Access-Control-Allow-Origin: *
  ```
* Use development proxy configurations if needed.

**RealEstatePro Example:**

* Ensure the backend server includes proper CORS headers.

---

## Tools for Integration

| Tool              | Purpose                                                      |
| ----------------- | ------------------------------------------------------------ |
| **Axios**         | REST client with support for interceptors and error handling |
| **Apollo Client** | GraphQL client with caching and state support                |
| **Postman**       | API testing and request inspection                           |
| **Firebase Auth** | Authentication service supporting email, 2FA, social login   |
| **Auth0**         | Secure authentication and role-based access control          |

**RealEstatePro Usage:**

* Use Axios to connect with backend endpoints.
* Test requests and responses with Postman.
* Authenticate users with Firebase or Auth0 as appropriate.

---

## Summary of Key Concepts

| Area                   | Summary                                                                 |
| ---------------------- | ----------------------------------------------------------------------- |
| **HTTP Requests**      | Understand and implement RESTful operations with headers and parameters |
| **Authentication**     | Secure apps with JWT, AsyncStorage, and optional 2FA                    |
| **API Integration**    | Connect with REST and GraphQL services using Axios or Apollo Client     |
| **Security & Caching** | Use HTTPS, caching, and throttling to improve performance and security  |
