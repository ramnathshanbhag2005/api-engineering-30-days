# Day 2 - REST APIs

Today I learned about REST APIs and how REST works with HTTP.

## What is REST?

REST stands for Representational State Transfer.

REST is an architectural style used for designing APIs that allow clients and servers to communicate over a network.

## Resources

REST APIs are generally designed around resources.

Examples:

- Students
- Courses
- Users
- Products

For example:

/students

## Endpoints

An endpoint is a specific API operation identified by an HTTP method and a path.

Examples:

GET /api/v1/students
GET /api/v1/students/25
POST /api/v1/students
PUT /api/v1/students/25
PATCH /api/v1/students/25
DELETE /api/v1/students/25

## HTTP Methods

GET - Retrieve data

POST - Create data

PUT - Replace or update a resource

PATCH - Partially update a resource

DELETE - Delete a resource

## Statelessness

REST follows a stateless interaction model. Each request should contain the information required by the server to process that request.

## REST vs SOAP

REST is an architectural style, while SOAP is a protocol.

REST commonly uses HTTP and often works with JSON. SOAP commonly uses XML-based messaging and follows a more formal messaging structure.

## Postman Practice

I used Postman to practice REST API requests.

I tested:

- GET all users
- GET a user by ID
- POST a user

I observed the request, response, status code, headers and JSON response body.

## API Design Practice

For a Student Management System, I designed the following endpoints:

GET /api/v1/students

GET /api/v1/students/25

POST /api/v1/students

PUT /api/v1/students/25

PATCH /api/v1/students/25

DELETE /api/v1/students/25

## Key Takeaway

Today I understood that REST API design is mainly about modeling resources and using appropriate HTTP methods to perform operations on those resources.
