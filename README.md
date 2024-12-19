# auth-statefull-vs-stateless
# Authentication: Stateless vs Stateful Concepts

This repository explains the concepts of stateless and stateful authentication using various techniques such as JWT tokens, cookies, session storage, and local storage. These concepts are critical for understanding modern authentication systems and securing web applications.

## Table of Contents
- [Overview](#overview)
- [Stateless Authentication](#stateless-authentication)
- [Stateful Authentication](#stateful-authentication)
- [Comparison of Techniques](#comparison-of-techniques)
- [Code Examples](#code-examples)
    - [JWT Tokens](#jwt-tokens)
    - [Cookies](#cookies)
    - [Session Storage](#session-storage)
    - [Local Storage](#local-storage)
- [Conclusion](#conclusion)

## Overview

In web applications, authentication is essential for securing user data and ensuring privacy. The terms **stateful** and **stateless** authentication describe how an application manages authentication data between the client and server.

- **Stateless Authentication:** The server does not store any session-related information between requests. Authentication information, like a JWT token, is typically stored on the client-side (in local storage or cookies).
  
- **Stateful Authentication:** The server maintains session-related information between requests, typically by using cookies or a server-side session store.

---

## Stateless Authentication

Stateless authentication is when the server does not retain any session information between requests. Instead, authentication data is stored on the client-side, such as in a **JWT (JSON Web Token)**. Every time a request is made, the client sends the JWT to the server, which then verifies the authenticity.

### Key Features:
- No server-side session storage.
- Authentication data is passed in the request.
- Often implemented using **JWT** (JSON Web Token).
- Simple to scale as the server does not need to remember any previous states or sessions.

---

## Stateful Authentication

In stateful authentication, the server maintains session-related information for the authenticated user. This session information can be stored on the server, while the client holds a **session ID** in cookies. Every time a request is made, the session ID is sent to the server, which uses it to look up session data.

### Key Features:
- The server maintains user sessions.
- **Cookies** or **Session ID** are used to identify sessions.
- Common for web applications that require more control over the user's session data (e.g., keeping track of login state on the server).

---

## Comparison of Techniques

| Feature                | Stateless Authentication (JWT)           | Stateful Authentication (Cookies / Sessions) |
| ---------------------- | --------------------------------------- | --------------------------------------------- |
| **Storage Location**    | Client-side (e.g., LocalStorage, Cookies) | Server-side, with Session ID in Cookies      |
| **Scalability**         | Easier to scale (no need to store state) | Harder to scale due to server-side storage  |
| **Security**            | Dependent on proper token management (JWT signature) | Session hijacking risk (e.g., if cookies not secure) |
| **Server Load**         | Low (server doesn’t store session data)  | Higher (server manages session data)          |
| **Session Expiry**      | Token expiry time encoded in JWT        | Session expiry handled by the server (timeout) |

---

## Code Examples

### JWT Tokens

A basic example of stateless authentication using JWTs.

```js
// Example: Signing JWT token
const jwt = require('jsonwebtoken');

// User login logic to generate JWT token
const user = { id: 1, username: 'testuser' };
const token = jwt.sign(user, 'secret_key', { expiresIn: '1h' });

console.log(token);

