# Cagtu Code of Conducts (API Guidelines)

**Table of contents**

- [Cagtu Code of Conducts (API Guidelines)](#cagtu-code-of-conducts-api-guidelines)
    - [REST Response Format](#rest-response-format)
    - [status codes](#status-codes)
    - [Success Response](#success-response)
        - [Create API Response](#create-api-response)
        - [List API Response](#list-api-response)
        - [Retrieve API Response](#retrieve-api-response)
        - [Update API Response](#update-api-response)
        - [Delete API Response](#delete-api-response)
    - [Error Response](#error-response)
        - [Validation Errors](#validation-errors)

## REST Response Format

- The response _should_ be in `JSON` format.
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

## status codes

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

## Success Response

When an API call is successful, the API should return the response with status codes less than 300 and greater than or
equal to 200.

The following is an example of a successful response:

### Create API Response

On success, create API would always respond with status code `201`. The response body would have the serializer data or
the content that has been passed during request by the client. The response body is generally used when the client-side
application want to render the content after creating a new item without further requesting to the server. We can
completely ignore the response body if we do not want it.

Example: post create: `POST /api/v1/posts/`

```json5
{
    "success": true,
    "message": "post has been successfully created",
    "data": {
        "id": 1,
        "title": "A blog post",
        "body": "Some useful content"
    }
}
```

### List API Response

List successful response are generally paginated. We have 2 popular methods of pagination, which are as follows

1. Page Number Pagination
2. Limit Offset Pagination

Generally, limit-offset pagination is preferred since the program do not need to do extra mathematics to find out the
next page number to paginate. It is also useful when we want to have offset based on data rather than primary key.

Example: post list: `GET /api/v1/posts/?limit=4&offset=100`

```json5
{
    "success": true,
    "next": "http://localhost:8001/api/v1/posts/?limit=4&offset=104",
    "previous": "http://localhost:8001/api/v1/posts/?limit=4&offset=96",
    "total": 1000,
    "data": [
        {
            "id": 100,
            "title": "A blog post",
            "body": "Some useful content"
        },
        {
            "id": 101,
            "title": "Another blog post",
            "body": "More content"
        },
        {
            "id": 102,
            "title": "Yet Another blog post",
            "body": "More content"
        },
        {
            "id": 103,
            "title": "Yet other blog post",
            "body": "More content"
        },
    ]
}
```

**Note**
_Even though list API do not find any values, the response can not have a response of 404 or any error response._
_Instead, It should respond with success response (status 200) and an empty list._

Example: Post list with no results: `GET /api/v1/posts/`

```json5
// The status code is still 200
{
    "success": true,
    "next": null,
    "previous": null,
    "total": 0,
    "data": []
}
```

### Retrieve API Response

Retrieve response is returned only when we want to know detail or want more information about the specific row or an
object in an ORM.

Example: Post detail by id: `GET /api/v1/posts/1/`

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

**Note**:
_Unlike **list response**, retrieve response will respond with an error response with status code 404 if the data is not
found._

### Update API Response

Update API (`PUT` / `PATCH`) generally responds with `200` status code. Generally the response would have the data from
the serializer, which we can completely ignore if we do not want them.

g: Post update by id: `PATCH /posts/1/`

```json5
{
    "success": true,
    "data": {
        "id": 1,
        "title": "A blog post",
        "body": "Some updated content"
    }
}
```

Any Error in updating the object should raise an exception which will respond with the error response which is explained
in [Error Response](#error-response) section.

### Delete API Response

Delete success API response will have status code `204`. 204 response means there is no content in the body. If
successfully deleted from the database, the server should respond with the code `204` without any content in the body
since the deleted data will already be destroyed and might not be available further for serializing.

However, if we are planning to perform `soft-delete` in the database, then we can respond with the id of the object (if
strictly required in the SRS document).

Any Error in deleting the object should raise an exception which will respond with the error response which is explained
in [Error Response](#error-response) section.

## Error Response

Error responses are returned when:

1. The client-side error occurs
2. The Server-side error occurs

- The key `success` should have the value `false`.
- Field specific errors should come in key value pairs.
- Non-Field errors can have error message in `message` key.
- Sometimes Non-Field errors can have key of `non_field_errors` with an array of values in it


### Validation Errors

Validation errors come in key-value pairs. The key is generally the field name and value will be an array of errors. (
even single error will be in array)

```json5
{
    "success": false,
    "message": "Some non-field error here",
    // sometimes message is not needed if error is descriptive itself.
    "errors": {
        "username": [
            "this username is already taken"
        ],
        "password": [
            "the password is too short"
        ]
    },
}
```

If a field has more than one validation errors, it still can be represented with this method.

**Example of a field-validation error response**

```json5
{
    "success": false,
    "errors": {
        "username": [
            "username already taken"
        ],
        "password": [
            "The password should contain at least 8 characters",
            "The password must have at least one special character, a number, and a capital letter"
        ],
    }
}
```

Sometimes validation error occurs between 2 fields. for example, we want to have `start_date` and `end_date` to take out
the statement of my spendings, but the difference might not be more than a month. In this case, we need to raise
non-field errors. The example of non-field error is shown in the example below:

**Example of a simple non-field error response**

```json5
{
    "success": false,
    "message": "Both Username and email fields are mandatory"
}
```

**Example of a response of non-field error with message**

```json5
{
    "success": false,
    "message": "date range is larger than expected",
    "non_field_errors": [
        "start and end dates should have maximum difference of 1 month"
    ]
}
```

**Example of a field-error and non-field error response**

```json5
{
    "success": false,
    "errors": {
        "username": [
            "This username is already used"
        ],
    "non_field_errors": [
        "The difference between 'start date' and 'end date' can not be more than a month"
    ]
    }
}
```
