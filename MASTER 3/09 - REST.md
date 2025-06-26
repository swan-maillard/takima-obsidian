---
cover: "[[rest.webp]]"
---
# 💠Table of Contents
```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 2 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```

---

# **💠 What is REST?** 

**REST (Representational State Transfer)** is an **architectural style** for designing web services that are **stateless**, **resource-based**, and operate over **HTTP**.

- Uses standard **HTTP methods** (GET, POST, PUT, DELETE, PATCH) for **CRUD** operations
    
- Resources are identified by **URIs** and represented in formats like **JSON or XML**.
    
- Each request is **self-contained**—the server does not store client state.
    
- Emphasizes **uniform interface** and **scalable, loosely-coupled** systems.

---

# **💠 Key principles

REST APIs must adhere to these  **5 key principles** to be truly RESTful:  
## 1. Resource Identification
- In REST, everything is treated as a **resource**, identified by a **unique URI** (Uniform Resource Identifier). 
- Resources represent **data objects** (e.g., `/users/42`), not actions. 

## 2. Uniform Interface  
A **consistent** way to interact with resources:  
- Relies on a **standardized set of operations** using HTTP methods (`GET`, `POST`, etc.).
- Uses **standard HTTP status codes** (e.g., 200 OK, 404 Not Found, 400 Bad Request) to indicate operation outcomes.
- This normalized interface ensures predictability and interoperability across clients and servers.
## 3. Statelessness
- Each REST request must contain **all necessary information** (auth, parameters, etc.) to be processed independently. 
- The server does **not store client session state** between requests. 
- This simplifies scaling and increases reliability by reducing server-side complexity.

## 4. Content Negotiation
- Supports **multiple representations** of a resource (e.g., JSON, XML)
- Clients and servers agree on representation format via:
	- `Accept` header (client preferences)
    - `Content-Type` header (actual format)

## 5. Hypermedia as the Engine of Application State (HATEOAS)
- RESTful responses can include **hypermedia links** to guide the client through available actions (e.g., links to update or delete a resource). 
- This makes the API more **self-descriptive** and **navigable**.
- Useful for **public API**.

---

# **💠 HTTP Methods in REST**  

| Method  | Description                      | Idempotent? |
| ------- | -------------------------------- | ----------- |
| GET     | Retrieve a resource              | Yes         |
| POST    | Create a resource or submit data | No          |
| PUT     | Update/replace a resource        | Yes         |
| PATCH   | Partial update of a resource     | No          |
| DELETE  | Remove a resource                | Yes         |
| HEAD    | Get headers (no body)            | Yes         |
| OPTIONS | List supported methods           | Yes         |

- **Idempotent**: Repeated requests have the same effect as a single request. 

---

# **💠 Status Codes in REST**  

There are five classes defined by the standard:

- **_1XX informational response_** – the request was received, continuing process
- **_2XX successful_** – the request was successfully received, understood, and accepted
- **_3XX redirection_** – further action needs to be taken in order to complete the request
- _**4XX client error_** – the request contains bad syntax or cannot be fulfilled
- _**5XX server error_** – the server failed to fulfil an apparently valid request

| Code | Meaning               | Usage                           |
| ---- | --------------------- | ------------------------------- |
| 200  | OK                    | Successful GET/PUT/PATCH/DELETE |
| 201  | Created               | Successful POST                 |
| 204  | No Content            | Success, but no response body   |
| 400  | Bad Request           | Invalid input                   |
| 401  | Unauthorized          | Missing/wrong authentication    |
| 403  | Forbidden             | Authenticated but no permission |
| 404  | Not Found             | Resource doesn’t exist          |
| 405  | Method Not Allowed    | Wrong HTTP method used          |
| 500  | Internal Server Error | Server-side failure             |

---

# **💠 Request & Response Headers**  

## 1. **Common Request Headers**  
  - `Accept`: Defines expected response format (`application/json`, `application/xml`).  
  - `Content-Type`: Specifies request body format.  
  - `Authorization`: For authentication (e.g., `Bearer <token>`).  
  
## 2. **Common Response Headers** 
  - `Content-Type`: Format of the response body.  
  - `Cache-Control`: Caching directives.  

---

# **💠 Authentication in REST APIs** 

- **Bearer Token (JWT)**: `Authorization: Bearer <token>`.  
- **OAuth 2.0**: Delegated authorization (e.g., `access_token`).  
- **API Keys**: Sent in headers or query params (less secure).  

---

# 💠 **Versioning**

Versioning helps manage **changes in APIs** without breaking existing clients. It is especially important in **mobile and frontend-backend development**, where old versions must continue working.

## 1. URL Path Versioning
Include the version in the URL
- `GET /api/v1/users`

## 2. Header Versioning
Specify the version in the `Accept` header.  
- Keeps URLs clean.  
- Slightly more complex for clients and caching.

## 3. Backward Compatibility
When adding new features or changes:
- Keep the **old version working**.
- Introduce the **new version in parallel**.
- Avoid breaking existing clients suddenly.

---

# 💠 Alternatives to REST

While REST is widely adopted for its simplicity and web-native design, there are notable alternatives suited for different use cases:

- **SOAP (Simple Object Access Protocol)** is a strict, XML-based protocol used in enterprise environments. Is heavier and more complex than REST.
    
- **GraphQL**, developed by Facebook, allows clients to **specify exactly what data they need**, reducing over-fetching and under-fetching common in REST.
    
- **gRPC**, from Google, is a high-performance, binary protocol based on **Protocol Buffers**. It's suited for internal microservices communication, with built-in support for streaming, contracts, and efficient serialization.