# Day 5/30 — JWT Fundamentals and Authentication

## Overview

Today, I explored authentication in backend engineering, focusing on session-based authentication and JSON Web Token (JWT)-based authentication.

The goal was to understand how servers identify authenticated users, how authentication state is maintained, and how to choose an appropriate authentication mechanism based on application requirements.

## 1. Why Authentication Is Needed

HTTP is stateless by default. Each request is independent, so a server does not automatically remember who made a previous request.

Authentication allows the server to establish the identity of a user. Authorization determines what that user is allowed to access or perform.

For example, in a Student Management System, a student may be allowed to view grades but not modify them.

## 2. Session-Based Authentication

In session-based authentication, the server maintains session information after a user successfully logs in.

### How It Works

1. The client sends login credentials to the server over HTTPS.
2. The server verifies the credentials.
3. The server creates a session and stores the associated user information.
4. The server sends the client a session ID, commonly through a cookie.
5. The browser sends the cookie with subsequent requests.
6. The server validates the session ID and identifies the user.

### Example

A session store might contain:

```text
Session ID: random-opaque-value
User ID: 101
Role: STUDENT
Expiry: configured expiration time
```

The browser holds the session ID, while the server maintains the associated session state.

### Advantages

- Straightforward session invalidation and logout.
- Centralized control over authentication state.
- Suitable for traditional web applications.
- Session data can be shared across multiple servers using a common session store.

### Challenges

- Requires session storage and lifecycle management.
- Distributed applications need an appropriate shared session store.
- Cookie-based authentication requires appropriate CSRF protections.

## 3. JWT-Based Authentication

JWT stands for JSON Web Token. It is a compact format for representing claims between parties.

A server can issue a signed JWT after successful authentication. The client then presents the token when accessing protected API endpoints.

### How It Works

1. The client sends login credentials.
2. The server verifies the credentials.
3. The server generates and signs a JWT.
4. The client receives the token.
5. The client sends the token with subsequent requests.
6. The server validates the token and its relevant claims.
7. The server checks authorization before allowing access to protected resources.

A common request header is:

```http
Authorization: Bearer <access_token>
```

### Structure of a JWT

A signed JWT typically consists of three parts:

```text
HEADER.PAYLOAD.SIGNATURE
```

**Header**

Contains metadata such as the token type and signing algorithm.

Example:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

**Payload**

Contains claims about the subject or token.

Example:

```json
{
  "sub": "student-101",
  "role": "STUDENT",
  "iat": 1791570000,
  "exp": 1791573600
}
```

**Signature**

Provides cryptographic integrity and allows the recipient to verify that the signed token has not been modified.

The timestamps above are illustrative examples.

### Important JWT Claims

| Claim | Purpose |
|---|---|
| `sub` | Identifies the subject |
| `iss` | Identifies the token issuer |
| `aud` | Identifies the intended recipient |
| `iat` | Records when the token was issued |
| `exp` | Specifies when the token expires |
| `nbf` | Specifies when the token becomes valid |
| `jti` | Provides a token identifier |

Not every application needs every registered claim.

### Advantages

- Token validation can be performed without a central session lookup on every request.
- Useful for certain distributed API architectures.
- Can carry identity-related claims.
- Supports interoperable token-based authentication when implemented correctly.

### Challenges

- Revocation before expiration requires additional design.
- Signing keys must be securely managed.
- Stolen tokens can be abused until they expire or are rejected.
- Tokens should not contain sensitive information in an ordinary signed payload.
- The server must validate the signature, expiration, and relevant claims.

A signed JWT is not automatically encrypted. Its payload can generally be decoded.

## 4. Session-Based Authentication vs JWT-Based Authentication

| Feature | Sessions | JWT access tokens |
|---|---|---|
| Authentication state | Maintained on the server | Claims carried in the token |
| Client credential | Usually a session ID | Usually an access token |
| Validation | Session lookup or equivalent | Cryptographic token validation |
| Immediate invalidation | Straightforward through session invalidation | Requires a revocation mechanism or current-state check |
| Distributed architecture | Requires appropriate shared session management | Can support verification across services with suitable key and trust configuration |
| Main considerations | Session storage and availability | Key management, expiration, revocation and token security |

Neither approach is universally better. The appropriate choice depends on the application's requirements and security model.

## 5. When Should Each Approach Be Used?

### Session-Based Authentication

A good default for many traditional browser applications where the server manages user sessions and immediate logout or invalidation is important.

### JWT-Based Authentication

Worth considering when an API architecture benefits from signed access tokens across independently deployed services or multiple client types.

JWT should not be chosen merely because it is popular. The architectural requirements should justify its use.

## 6. Browser Security Considerations

When authentication credentials are stored in cookies:

- `Secure` restricts cookie transmission to HTTPS.
- `HttpOnly` prevents JavaScript from directly reading the cookie.
- `SameSite` helps control cross-site cookie sending.
- CSRF protections should be selected according to the application's design.

When bearer tokens are stored in browser-accessible storage, an XSS vulnerability may expose them to malicious JavaScript.

Authentication design should include HTTPS, secure credential handling, appropriate token or session expiration, and authorization checks on protected operations.

## 7. Practical Example: Student Management API

Consider a system with the following endpoints:

| Endpoint | Purpose |
|---|---|
| `POST /api/auth/login` | Authenticate a user |
| `GET /api/students` | Retrieve student records |
| `GET /api/students/{id}/grades` | View a student's grades |
| `PATCH /api/students/{id}` | Update permitted student information |

Authentication establishes who is making the request. Authorization determines whether that user can access the requested resource or perform the operation.

For example, an administrator may be allowed to update grades, while a student may only be allowed to view their own grades.

## 8. Important Backend Engineering Insight

Consider a requirement where an administrator disables a user's account and the user must immediately lose access.

With sessions, the server can invalidate the session centrally.

With JWT, the server may need to check current account status, use a token revocation mechanism, or apply another strategy that ensures subsequent requests are rejected.

This introduces an architectural trade-off between token validation without a central lookup and immediate control over authentication state.

The correct solution depends on the application's security and consistency requirements.

## 9. Key Learnings

- HTTP is stateless by default.
- Authentication and authorization are different concepts.
- Sessions maintain server-side authentication state.
- JWTs carry claims and can be cryptographically signed.
- A signed JWT is not automatically encrypted.
- Expiration, revocation, and secure credential storage are important.
- Cookies and bearer tokens have different security considerations.
- Authentication mechanisms should be chosen based on requirements, not trends.

## 10. Day 6 Plan

The next session will focus on implementing JWT authentication using Java and Spring Boot.

Planned practical work:

1. Configure the Spring Boot project.
2. Implement a login endpoint.
3. Generate a signed JWT.
4. Protect an API endpoint using Spring Security.
5. Test valid, invalid, and expired tokens in Postman.
6. Understand token validation and error responses.
7. Document the implementation and lessons learned.

**Status:** Day 5 — Concepts and design trade-offs studied. Practical implementation is planned for Day 6.

---

## Reflection

Today's learning reinforced that backend engineering is not only about writing code. It also involves understanding trade-offs, security requirements, and the operational consequences of architectural decisions.

The next step is to translate these concepts into a working implementation.
