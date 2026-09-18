# Day 3 - API Request and Response Anatomy

Today I learned more about how API requests and responses actually work.

## 1. URL Anatomy

Example:

https://jsonplaceholder.typicode.com/users/1

- Scheme -> https
- Host -> jsonplaceholder.typicode.com
- Path -> /users/1

The path can be used to identify a particular resource.

## 2. Headers

Headers contain metadata/information about the request or response.

Example:

Content-Type: application/json

This tells the server that the incoming data is formatted as JSON.

Other common headers:

- Accept
- Authorization
- Content-Type

## 3. Request Body

The request body contains the actual data sent from the client to the server.

Example:

{
  "name": "Ramnath",
  "branch": "ISE"
}

Request body is commonly used with POST, PUT and PATCH requests.

## 4. Response Body

The response body contains the data sent back by the server.

Example:

{
  "id": 101,
  "name": "Ramnath",
  "branch": "ISE"
}

The server can generate an ID for newly created data and return it in the response.

## 5. Collection and Single Resource

GET /users

This represents a collection of users.

GET /users/1

This represents a specific user.

So:

/users -> collection

/users/1 -> specific resource

## 6. Path Parameters

Path parameters are used to identify a specific resource.

Example:

GET /students/25

Here 25 is used to identify the student.

## 7. Query Parameters

Query parameters can be used for filtering, searching, sorting or controlling the result.

Example:

GET /students?branch=ISE

This gets students from the ISE branch.

Multiple query parameters can also be used:

GET /students?branch=ISE&semester=6

Example for pagination:

GET /students?limit=10&page=2

This can be used to get 10 students from page 2.

## 8. JSON

JSON is commonly used for sending and receiving data in APIs.

JSON Object:

{
  "id": 1,
  "name": "Ramnath"
}

JSON Array:

[
  {
    "id": 1,
    "name": "Ramnath"
  },
  {
    "id": 2,
    "name": "Rahul"
  }
]

JSON can also contain nested objects.

Example:

{
  "name": "Ramnath",
  "address": {
    "city": "Mysuru"
  }
}

## 9. Postman Practice

I used Postman to test a public API.

Request:

GET https://jsonplaceholder.typicode.com/users

The server returned a JSON array containing user objects.

I also tested:

GET https://jsonplaceholder.typicode.com/users/1

which returned a single user.

I then used the Params section in Postman and added:

_limit = 3

The request became:

GET https://jsonplaceholder.typicode.com/users?_limit=3

The response contained 3 user objects.

## 10. Student API Examples

GET /students
-> Get all students

GET /students/25
-> Get student with ID 25

GET /students?branch=ISE
-> Get students from ISE branch

GET /students?limit=10&page=2
-> Get 10 students from page 2

## Key Takeaway

Today I understood the different parts of an API request and response and practiced them using Postman.

I also learned the difference between path parameters and query parameters and how JSON data is structured.
