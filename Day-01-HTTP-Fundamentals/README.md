# Day 1 — HTTP Fundamentals

## What I Learned

### Client

A client is a system that sends a request to a server.

Examples:
- Browser
- Postman
- Mobile application

### Server

A server receives the request, processes it, and sends a response back to the client.

### API

An API provides an interface through which a client can communicate with a server.

### HTTP

HTTP is a communication protocol used for exchanging requests and responses between a client and a server.

## HTTP Methods

- GET — Retrieve data
- POST — Create or submit data
- PUT — Update or replace data
- PATCH — Partially update data
- DELETE — Delete data

## HTTP Status Codes

- 200 OK — Request was successfully processed
- 201 Created — A new resource was successfully created
- 404 Not Found — The requested resource could not be found
- 500 Internal Server Error — The server encountered an error

## API Endpoint

An API endpoint is a specific address through which an API receives requests for a particular resource or operation.

Examples:

GET /users

GET /users/1

## Request-Response Flow

Client
↓
HTTP Request
↓
Server
↓
Processing
↓
HTTP Response
↓
Client

## Practical Work

Used Postman to send GET and POST requests to a public testing API and inspected the response status, headers, and body.

## Key Takeaway

An API allows a client and server to communicate through requests and responses. HTTP provides the communication rules, while different HTTP methods describe the operation being requested.
