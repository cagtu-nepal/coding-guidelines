# Cagtu Code of Conducts

## API Guidelines

**Table of contents**
- [Cagtu Code of Conducts](#cagtu-code-of-conducts)
  - [API Guidelines](#api-guidelines)
    - [REST Response Format](#rest-response-format)
    - [status codes](#status-codes)
    - [**Success Response**](#success-response)
    - [Error Response](#error-response)
    - [Delete Success](#delete-success)
    - [validation errors](#validation-errors)


### REST Response Format

- The response should be in `JSON` format.
- `Content-Type` header must have value `application/json`.
- Each non-paginated response should contain `success` and `data`
- Each paginated response should contain `success`, `next`, `previous`, `total` and `data`.
- Each Error response should contain `success: false`, `message` and `errors`
- Default Page size should be 15
- Default pagination should be `limit-offset` pagination.
- Listing from the paginated response should have 200 response even if the results is empty array.
- If we are retrieving specific data eg: `/posts/1/` and detail is not found, then 404 response should be returned.

Basic JSON Response should be in the following format:

```json5
{
  "success": true,
  // or false
  "data": {
    //    "content will be either json object or array or primary data type."
  }
}
```

### status codes

| Action               | Status Text           | Code  | Remarks            |
| -------------------- | --------------------- | :---: | ------------------ |
| `GET` `PUT` `PATCH`  | Success               |  200  | `list`, `retrieve` |
| `GET` `PUT` `PATCH`  | Not Found             |  404  |                    |
| `POST`               | Success               |  201  | Created            |
| `POST` `PUT` `PATCH` | Validation Error      |  400  | Bad Request        |
| `DELETE`             | Success               |  204  | No Content         |
| all                  | Unauthorized          |  401  |                    |
| all                  | Permission Denied     |  403  |                    |
| all                  | Internal Server Error |  500  |                    |

### **Success Response**

When an API call is successful, the API should return the response with status codes less than 300 and greater than or equal to 200.

The following is an example of  a successful response:

**Paginated Response (List API)**

Eg: post list: `GET /posts/?page=4`

```json5
{
  "success": true,
  "next": "http://localhost:8001/api/post/?page=5",
  "previous": "http://localhost:8001/api/post/?page=3",
  "total": 1000,
  "data": [
    {
      "id": 1,
      "title": "A blog post",
      "body": "Some useful content"
    },
    {
      "id": 2,
      "title": "Another blog post",
      "body": "More content"
    },
  ]
}
```

**Response by ID (Retrieve API)**
Eg: Post detail by id: `GET /posts/1/`

```json5
{
  "success": true,
  "data": {
    "id": 1,
    "title": "A blog post",
    "body": "Some useful content"
  }
}
```

### Error Response

Error responses are returned when:
1. The client-side error occurs
2. The Server-side error occurs

- The key `success` should have the value `false`.
- Field specific errors should come in key value pairs.
- Non-Field errors can have error message in `message` key.

**Example of a field validation error response**
```json5
{
  "success": false,
  "errors": {
    "username": [
        "Username already Taken"
        ]    "password": [
        "The password should contain at least 8 characters",
        "The password must have at least one special character, number, and a capital letter".
    ],

  }
}
```

**Example of a non-field error response**
```json5
{
  "success": false,
  "message": "Both Username and email fields are mandatory",
}
```

### Delete Success

Delete success response will have status code `204`. 204 response means there is no content in the body.

### validation errors

Validation errors come in key-value pairs. The key is generally the field name and value will be in array or errors. (
even single error will be in array)

```json5
{
  "success": false,
  "message": "Some non-field error here",
  "errors": {
    "username": [
      "This username is already used"
    ]
  },
}
```
