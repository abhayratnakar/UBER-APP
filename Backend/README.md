# User Registration Endpoint

## POST /users/register

### Description
This endpoint is used to register a new user. It requires the user's first name, last name, email, and password.

### Request Body
The request body should be a JSON object containing the following fields:
- `fullname`: An object containing:
  - `firstname`: The user's first name (minimum 3 characters).
  - `lastname`: The user's last name (minimum 3 characters, optional).
- `email`: The user's email address (must be a valid email).
- `password`: The user's password (minimum 6 characters).

### Example Request
```json
{
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john.doe@example.com",
  "password": "password123"
}
```

### Responses

#### Success
- **Status Code**: 201 Created
- **Response Body**:
  ```json
  {
    "token": "jwt-token",
    "user": {
      "_id": "user-id",
      "fullname": {
        "firstname": "John",
        "lastname": "Doe"
      },
      "email": "john.doe@example.com"
    }
  }
  ```

#### Validation Errors
- **Status Code**: 400 Bad Request
- **Response Body**:
  ```json
  {
    "errors": [
      {
        "msg": "Error message",
        "param": "parameter",
        "location": "body"
      }
    ]
  }
  ```

### Notes
- The `password` field is hashed before being stored in the database.
- The `token` field in the response is a JWT token that can be used for authentication.

# User Login Endpoint

## POST /users/login

### Description
This endpoint is used to log in an existing user. It requires the user's email and password.

### Request Body
The request body should be a JSON object containing the following fields:
- `email`: The user's email address (must be a valid email).
- `password`: The user's password (minimum 6 characters).

### Example Request
```json
{
  "email": "john.doe@example.com",
  "password": "password123"
}
```

### Responses

#### Success
- **Status Code**: 200 OK
- **Response Body**:
  ```json
  {
    "token": "jwt-token",
    "user": {
      "_id": "user-id",
      "fullname": {
        "firstname": "John",
        "lastname": "Doe"
      },
      "email": "john.doe@example.com"
    }
  }
  ```

#### Validation Errors
- **Status Code**: 400 Bad Request
- **Response Body**:
  ```json
  {
    "errors": [
      {
        "msg": "Error message",
        "param": "parameter",
        "location": "body"
      }
    ]
  }
  ```

#### Authentication Errors
- **Status Code**: 401 Unauthorized
- **Response Body**:
  ```json
  {
    "message": "Invalid email or password"
  }
  ```

### Notes
- The `password` field is hashed before being compared with the stored password.
- The `token` field in the response is a JWT token that can be used for authentication.

# User Profile Endpoint

## GET /users/profile

### Description
This endpoint is used to get the profile of the authenticated user.

### Responses

#### Success
- **Status Code**: 200 OK
- **Response Body**:
  ```json
  {
    "_id": "user-id",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com"
  }
  ```

#### Authentication Errors
- **Status Code**: 401 Unauthorized
- **Response Body**:
  ```json
  {
    "message": "Unauthorized"
  }
  ```

### Notes
- This endpoint requires a valid JWT token in the `Authorization` header or `token` cookie.

# User Logout Endpoint

## GET /users/logout

### Description
This endpoint is used to log out the authenticated user.

### Responses

#### Success
- **Status Code**: 200 OK
- **Response Body**:
  ```json
  {
    "message": "Logged out successfully"
  }
  ```

#### Authentication Errors
- **Status Code**: 401 Unauthorized
- **Response Body**:
  ```json
  {
    "message": "Unauthorized"
  }
  ```

### Notes
- This endpoint requires a valid JWT token in the `Authorization` header or `token` cookie.
- The token is blacklisted after logout to prevent reuse.