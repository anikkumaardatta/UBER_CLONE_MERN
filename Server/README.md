# Uber Clone MERN API Documentation

## User Registration Endpoint

### POST /users/register

**Description:**  
This endpoint allows users to register a new account by providing their personal details. The system validates the input data, hashes the password, creates a new user in the database, and returns an authentication token along with the user details.

**Request Body:**  
The request must be sent as JSON with the following required fields:

- `fullName` (object): An object containing the user's first and last name.
  - `firstName` (string): The user's first name. Must be at least 3 characters long.
  - `lastName` (string): The user's last name. Must be at least 3 characters long.
- `email` (string): A valid email address. Must be a properly formatted email.
- `password` (string): The user's password. Must be at least 8 characters long.

**Example Request Body:**

```json
{
  "fullName": {
    "firstName": "John",
    "lastName": "Doe"
  },
  "email": "john.doe@example.com",
  "password": "securepassword123"
}
```

**Response:**

- **201 Created:** User successfully registered.
  - **Body:**
    ```json
    {
      "token": "jwt_authentication_token_here",
      "user": {
        "_id": "user_id",
        "fullName": {
          "firstName": "John",
          "lastName": "Doe"
        },
        "email": "john.doe@example.com"
      }
    }
    ```

- **400 Bad Request:** Validation errors in the request body.
  - **Body:**
    ```json
    {
      "errors": [
        {
          "msg": "Invalid email address!",
          "param": "email",
          "location": "body"
        },
        {
          "msg": "First name must be at least 3 characters long.",
          "param": "fullName.firstName",
          "location": "body"
        },
        {
          "msg": "Last name must be at least 3 characters long.",
          "param": "fullName.lastName",
          "location": "body"
        },
        {
          "msg": "Password must be at least 8 characters long.",
          "param": "password",
          "location": "body"
        }
      ]
    }
    ```

**Notes:**

- All fields are required.
- The password is hashed before storing in the database.
- A JWT token is generated and returned for authentication.
- The user model includes additional fields like `socketId`, but they are not required for registration.
