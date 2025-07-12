# RESTful Services Fundamentals

## Statelessness in REST
- **Definition**: Statelessness is a core principle of REST (Representational State Transfer) architecture, meaning each request from a client to a server must contain all the information needed to process the request. The server does not store information about the client’s state between requests.
- **Implications**:
  - Each request is independent, improving scalability and reliability.
  - The client must include authentication details, parameters, or session data in every request (e.g., via tokens or headers).
  - Example: A REST API for retrieving user data requires a user ID and authentication token in every `GET /users/{id}` request, rather than relying on server-side session storage.
- **Benefits**:
  - Simplifies server design, as no session state needs to be managed.
  - Enhances scalability, as requests can be handled by any server instance in a distributed system.
- **Challenges**:
  - Clients must send more data per request, increasing payload size.
  - Authentication must be handled explicitly (e.g., using JWT or OAuth).

## Characteristics of RESTful APIs
- **Key Features**:
  - **Stateless**: As described above, each request is self-contained.
  - **Client-Server Architecture**: Separates client (frontend) and server (backend), enabling independent evolution of each.
  - **Use of HTTP Methods**: Standard methods like GET, POST, PUT, DELETE, and PATCH are used to perform CRUD (Create, Read, Update, Delete) operations.
  - **Resource-Based**: Resources (e.g., users, orders) are identified by unique URIs (e.g., `/users/123`).
  - **Layered System**: Allows intermediaries like proxies or load balancers without affecting client-server interaction.
  - **Cacheable**: Responses can be cached to improve performance, using headers like `Cache-Control`.
- **What is NOT a Characteristic**:
  - **Session Storage on Server**: REST APIs do not rely on server-side session storage, as this violates statelessness. Instead, session data is managed client-side (e.g., via tokens).
**Example**: A RESTful API for a blog might use `GET /posts` to retrieve posts, `POST /posts` to create a new post, and `DELETE /posts/123` to delete a specific post, with no server-side session storage.

## Resource Identification
- **Concept**: In REST, every resource (e.g., a user, product, or order) is uniquely identified by a URI (Uniform Resource Identifier).
- **URI Structure**: Typically follows a hierarchical format, e.g., `/api/v1/users/123/orders/456`.
- **Best Practices**:
  - Use nouns for resources (e.g., `/users` instead of `/getUsers`).
  - Include resource IDs for specific instances (e.g., `/users/123`).
  - Use query parameters for filtering or pagination (e.g., `/users?role=admin`).
**Example**: In a library API, a book resource might be accessed via `GET /books/978-3-16-148410-0`, where the ISBN uniquely identifies the book.

## HTTP Methods
- **GET**: Retrieves data from the server (e.g., `GET /users/123` fetches user details). Idempotent and safe.
- **POST**: Submits data to create a new resource (e.g., `POST /users` with a JSON payload to create a user). Not idempotent.
- **PUT**: Updates an existing resource or creates it if it doesn’t exist (e.g., `PUT /users/123` updates user details). Idempotent.
- **DELETE**: Removes a resource (e.g., `DELETE /users/123` deletes a user). Idempotent.
- **PATCH**: Partially updates a resource (e.g., `PATCH /users/123` updates only the user’s email).
**Example**: A REST API for a to-do list might use:
  - `GET /tasks` to list all tasks.
  - `POST /tasks` to create a new task.
  - `DELETE /tasks/123` to delete a task.

## HTTP Status Codes
- **Definition**: Numeric codes returned in HTTP responses to indicate the outcome of a request.
- **Common Codes**:
  - **200 OK**: Request was successful (e.g., successful `GET` or `PUT`).
  - **201 Created**: Resource created successfully (e.g., after `POST`).
  - **204 No Content**: Request successful, no response body (e.g., after `DELETE`).
  - **400 Bad Request**: Invalid request syntax or parameters.
  - **401 Unauthorized**: Authentication required or failed.
  - **404 Not Found**: Resource not found.
  - **500 Internal Server Error**: Server-side error.
**Example**: A successful `GET /users/123` returns `200 OK` with the user’s data in the response body.