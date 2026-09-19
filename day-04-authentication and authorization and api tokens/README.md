# Day 4 - Authentication and Authorization

Today I learned how APIs authenticate users, authorize access, and protect API resources.

## Topics Covered

- Authentication
- Authorization
- API Keys
- Tokens
- Authorization Header
- Bearer Authentication Scheme
- 401 Unauthorized
- 403 Forbidden
- Protected API Resources
- Token-based Authentication Flow
- How the Server Identifies the User Using a Token

---

## 1. Authentication

Authentication means verifying who the user is.

For example, when a user logs into an application using a username and password, the server verifies the credentials.

Example:

```http
POST /login
{
  "username": "ramnath",
  "password": "mypassword"
}

If the credentials are correct, the user is authenticated.

Authentication = Who are you?

2. Authorization

Authorization means checking what an authenticated user is allowed to do.

For example, a normal student may be allowed to view their profile, while an admin may be allowed to access and manage all users.

Authorization = What are you allowed to do?

Example
Login credentials → Authentication

Permission to transfer money → Authorization

Authentication happens first because the server needs to know who the user is before checking their permissions.

3. API Keys

An API key is a credential commonly used to identify an application or API consumer and control access to an API.

API keys are commonly sent in request headers.

Example:

X-API-Key: 12345abc

The server can validate the API key before processing the request.

Important

Real API keys should never be committed to a public GitHub repository.

They should be stored using environment variables or other secure methods.

4. Tokens

After successful authentication, a server can provide a token to the client.

Example:

POST /login

Response:

{
  "token": "abc123"
}

The client can then use this token when accessing protected resources.

Example:

GET /profile
Authorization: Bearer abc123

The client does not need to send the username and password again with every request.

The token acts as a credential for subsequent authenticated requests.

5. Authorization Header

The token is commonly sent using the HTTP Authorization header.

Example:

Authorization: Bearer abc123

The header contains:

Authorization → HTTP header

Bearer → Authentication scheme

abc123 → Token
6. Bearer Authentication Scheme

Bearer is an authentication scheme used with the Authorization header.

Authorization: Bearer abc123

The idea is that the client presents the token as a credential when making a protected request.

Movie Ticket Analogy

A token can be compared to a movie ticket.

You cannot enter the theatre simply because you bought a ticket earlier. You need to present the ticket at the entrance.

Similarly, after login, the client presents the token when accessing a protected API.

Movie Theatre → API Server

Movie Ticket → Token

Present Ticket → Send Token

Ticket Verification → Token Validation
7. 401 Unauthorized

401 Unauthorized generally indicates an authentication problem.

It can occur when:

Authentication credentials are missing
The token is invalid
The authentication credential cannot be accepted

Example:

GET /profile

Without valid authentication, the server may return:

401 Unauthorized

Simple meaning:

The server cannot properly authenticate the request.

8. 403 Forbidden

403 Forbidden means that the user has been authenticated but does not have sufficient permission to access the requested resource.

Example:

GET /admin/users
Authorization: Bearer abc123

Suppose the token is valid and belongs to a normal student.

The server knows who the user is, but the user does not have the required admin permission.

The server can return:

403 Forbidden

Simple meaning:

The server knows who you are, but you are not allowed to access this resource.

9. 401 vs 403

The main difference is:

401 → Authentication problem

403 → Permission / Authorization problem

Example:

No valid authentication
        ↓
401 Unauthorized

Whereas:

Valid authentication
        ↓
Insufficient permissions
        ↓
403 Forbidden
10. Protected API Resources

Not every API endpoint has to be public.

Some endpoints can require authentication.

Example:

GET /products

could be publicly accessible.

But:

GET /profile

may require authentication.

An administrative endpoint such as:

GET /admin/users

may require both:

Authentication
Admin authorization

This allows APIs to protect sensitive resources.

11. Basic Token-Based Authentication Flow

A basic token-based authentication flow is:

User
  ↓
Username + Password
  ↓
POST /login
  ↓
Server verifies credentials
  ↓
Authentication successful
  ↓
Token generated
  ↓
Client receives token
  ↓
Client sends token with protected requests
  ↓
Server validates token
  ↓
Request accepted or rejected
12. How the Server Uses the Token

Suppose login is successful:

POST /login

The server returns:

{
  "token": "abc123"
}

Later, the client sends:

GET /profile
Authorization: Bearer abc123

The server receives the token and validates it.

The token is associated with an authenticated user or session.

If the token is valid, the server can determine which authenticated user or session it represents and process the request.

If the token is invalid or missing, the server can reject the request.

13. Example: Banking Application

Consider a banking API.

Login
POST /login
{
  "username": "ramnath",
  "password": "mypassword"
}

The server verifies the credentials.

Token Response
{
  "token": "abc123"
}
Access Profile
GET /profile
Authorization: Bearer abc123

The server validates the token and processes the request if it is valid.

Transfer Money
POST /transfer
Authorization: Bearer abc123

The server can first authenticate the user and then check whether the user has permission to perform the transfer.

This demonstrates the difference between authentication and authorization.

14. API Key vs Token
API Key	Token
Commonly identifies an application or API consumer	Commonly represents an authenticated user or session
Often used for API access and usage control	Commonly used for authenticated requests
Example: X-API-Key	Example: Authorization: Bearer <token>
Should be kept secure	Should also be kept secure

The exact implementation depends on the API design.

15. Key Takeaways

Today I learned that:

Authentication verifies the identity of a user.
Authorization checks what an authenticated user is allowed to access.
API keys can be used as credentials for API access.
Tokens can be used for authenticated API requests.
Tokens are commonly sent through the Authorization header.
Bearer is an authentication scheme used with bearer tokens.
401 Unauthorized generally indicates an authentication problem.
403 Forbidden indicates insufficient permission.
Protected API resources can require authentication and authorization.
A token allows the client to make authenticated requests without repeatedly sending the original username and password.
Day 4 Summary
Authentication
      ↓
Who are you?

Authorization
      ↓
What are you allowed to do?

API Key
      ↓
Credential for API access

Token
      ↓
Credential for authenticated requests

Bearer
      ↓
Authentication scheme

401
      ↓
Authentication problem

403
      ↓
Permission problem
