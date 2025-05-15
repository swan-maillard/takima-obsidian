## **1. What is REST?** 

- **REST (Representational State Transfer)** is an **architectural style** for building scalable and maintainable web services.  

- It is based on **stateless, client-server communication**, where each request from the client contains all the necessary information for the server to process it, typically using **HTTP/HTTPS**.  

- REST leverages **standard HTTP methods** (GET, POST, PUT, DELETE, PATCH, etc.) to perform **CRUD (Create, Read, Update, Delete)** operations on resources, which are identified by **URIs (Uniform Resource Identifiers)**.  

- Unlike traditional RPC-style APIs, REST emphasizes **resource-oriented design**, where data (e.g., users, products) is treated as entities that can be manipulated via a uniform interface.  

---

## **2. The  Key Principles of REST

REST APIs must adhere to these  **core constraints** to be truly RESTful:  

#### **2. Statelessness**  
- **No server-side session state**: Each request must contain **all necessary data** (e.g., authentication tokens, request parameters).  
- **Benefits**:  
  - Improves **scalability** (servers don’t store client context).  
  - Simplifies **load balancing** (any server can handle any request).  

#### **3. Cacheability**  
- Responses must **explicitly define** if they can be cached (via HTTP headers like `Cache-Control`).  
- **Benefits**:  
  - Reduces server load (clients reuse cached responses).  
  - Improves performance (e.g., `GET /products` can be cached).  

#### **4. Uniform Interface**  
A consistent way to interact with resources:  
- **Resource Identification**: Each resource has a **unique URI** (e.g., `/users/123`).  
- **Resource Manipulation via Representations**: Clients interact via **representations** (JSON, XML) rather than direct data access.  
- **Self-descriptive Messages**: Requests/responses include metadata (e.g., `Content-Type: application/json`).  

#### **5. Content Negotiation**
- Clients and servers agree on representation format via:
	- `Accept` header (client preferences)
    - `Content-Type` header (actual format)
- Supports multiple formats (JSON, XML, YAML, etc.)

#### **6. Layered System**  
- Clients interact with an **intermediary layer** (e.g., API gateways, proxies) without knowing backend complexity.  
- **Benefits**:  
  - Enables **security layers** (firewalls, rate limiting).  
  - Supports **scalability** (load balancers, CDNs).  

---

## **3. REST vs. SOAP**  

**SOAP**, originally an acronym for **Simple Object Access Protocol**, is a messaging protocol specification for exchanging structured information in the implementation of web services It uses XML for data format.

| Feature      | REST                    | SOAP                      |
| ------------ | ----------------------- | ------------------------- |
| Protocol     | HTTP/HTTPS              | HTTP, SMTP, etc.          |
| Data Format  | JSON, XML, Plain Text   | XML only                  |
| Statefulness | Stateless               | Stateful (WS-* standards) |
| Performance  | Lightweight, faster     | Heavy due to XML          |
| Flexibility  | More flexible, scalable | Strict standards          |

---

## **4. HTTP Methods in REST**  

| Method  | Description                      | Idempotent? | Safe? |
| ------- | -------------------------------- | ----------- | ----- |
| GET     | Retrieve a resource              | Yes         | Yes   |
| POST    | Create a resource or submit data | No          | No    |
| PUT     | Update/replace a resource        | Yes         | No    |
| PATCH   | Partial update of a resource     | No          | No    |
| DELETE  | Remove a resource                | Yes         | No    |
| HEAD    | Get headers (no body)            | Yes         | Yes   |
| OPTIONS | List supported methods           | Yes         | Yes   |

- **Idempotent**: Repeated requests have the same effect as a single request.  
- **Safe**: Does not modify the resource (e.g., GET, HEAD, OPTIONS).  

---

## **5. RESTful URI Design Best Practices**  

- Use **nouns** (not verbs) for resources:  
  - ✅ `/users` (Good)  
  - ❌ `/getUsers` (Bad)  
- Use **plural nouns** for collections.  
- Use **hyphens (-)** for readability, not underscores (_).  
- Use **lowercase letters**.  
- Avoid **file extensions** (e.g., `.json`), use `Accept` header instead.  
- Use **query params for filtering**: `/users?role=admin`.  
- Use **sub-resources for relationships**: `/users/123/posts`.  

---

## **6. Status Codes in REST**  

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

## **7. Request & Response Headers**  

- **Common Request Headers**:  
  - `Accept`: Defines expected response format (`application/json`, `application/xml`).  
  - `Content-Type`: Specifies request body format.  
  - `Authorization`: For authentication (e.g., `Bearer <token>`).  
  
- **Common Response Headers**:  
  - `Content-Type`: Format of the response body.  
  - `Cache-Control`: Caching directives.  

---

## **8. Authentication in REST APIs** 

- **Basic Auth**: `Authorization: Basic <base64(username:password)>` (Not secure without HTTPS).  
- **Bearer Token (JWT)**: `Authorization: Bearer <token>`.  
- **OAuth 2.0**: Delegated authorization (e.g., `access_token`).  
- **API Keys**: Sent in headers or query params (less secure).  

---

## **9. HATEOAS (Hypermedia as the Engine of Application State)**  

- Responses include **links** to related actions (e.g., `next`, `prev`).  
- Example:  
  ```json
  {
    "id": 123,
    "name": "John",
    "links": [
      { "rel": "self", "href": "/users/123" },
      { "rel": "posts", "href": "/users/123/posts" }
    ]
  }
  ```

---

## **10. Common Interview Questions**  

1. **What makes an API RESTful?**  
   - Follows REST principles (stateless, uniform interface, etc.).  
2. **Difference between PUT and PATCH?**  
   - PUT replaces the entire resource; PATCH updates partially.  
3. **How to handle versioning in REST APIs?**  
   - URL path (`/v1/users`), headers (`Accept: application/vnd.company.v1+json`).  
4. **What is idempotency? Why is it important?**  
   - Ensures repeated calls don’t cause unintended side effects (critical for retries).  
5. **How does REST differ from GraphQL/gRPC?**  
   - REST uses fixed endpoints, while GraphQL allows query flexibility.  