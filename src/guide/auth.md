# Authentication Endpoints

## Login

To authenticate a user, send a POST request to the following URL:

```txt
https://hypersend.co.mz/api/login
```

### Request Body

| Key      | Description          | Required | Example            |
| -------- | -------------------- | -------- | ------------------ |
| email    | User's email address | Yes      | "user@example.com" |
| password | User's password      | Yes      | "secret123"        |

Example JSON object for the request body:

```json
{
  "email": "user@example.com",
  "password": "secret123"
}
```

### Response Structure

For successful login, the response structure is:

```json
{
  "success": true,
  "data": {
    "user": {
      "id": 1,
      "name": "User Example",
      "email": "user@example.com",
      "email_verified_at": null,
      "two_factor_confirmed_at": null,
      "current_team_id": null,
      "profile_photo_path": null,
      "created_at": "2023-08-02T10:12:00.000000Z",
      "updated_at": "2023-08-02T10:12:00.000000Z",
      "profile_photo_url": ""
    },
    "token": "4|VhtSbF8b9gvpjUQoJrXXjTdkSkMXcxMKXe3UsGQD"
  }
}
}
```

- `access_token`: Bearer token for authentication.
- `token_type`: Token type (usually "bearer").
- `expires_in`: Token expiration time in 30 days.

For unsuccessful login, the response structure is:

```json
{
  "success": false,
  "message": "Invalid credentials"
}
```

## Register

To create a new user, send a POST request to the following URL:

```txt
https://hypersend.co.mz/api/register
```

### Request Body

| Key        | Description          | Required | Example            |
| ---------- | -------------------- | -------- | ------------------ |
| name       | User's name          | Yes      | "John Doe"         |
| email      | User's email address | Yes      | "user@example.com" |
| password   | User's password      | Yes      | "secret123"        |
| c_password | Confirm password     | Yes      | "secret123"        |

Example JSON object for the request body:

```json
{
  "name": "John Doe",
  "email": "user@example.com",
  "password": "secret123",
  "c_password": "secret123"
}
```

### Response Structure

For successful registration, the response structure is:

```json
{
  "success": true,
  "message": "Registration successful",
  "data": {
    "user": {
      "id": 1,
      "name": "User Example",
      "email": "user@example.com",
      "email_verified_at": null,
      "two_factor_confirmed_at": null,
      "current_team_id": null,
      "profile_photo_path": null,
      "created_at": "2023-08-02T10:12:00.000000Z",
      "updated_at": "2023-08-02T10:12:00.000000Z",
      "profile_photo_url": ""
    }
  }
}
```

For unsuccessful registration, the response structure is similar to the unsuccessful login response.

## Logout

To log out a user, send a POST request to the following URL:

```txt
https://hypersend.co.mz/api/logout
```

### Response Structure

For successful logout, the response structure is:

```json
{
  "success": true,
  "message": "Logout successful"
}
```

## User Profile

To retrieve the authenticated user's profile, send a GET request to the following URL:

```txt
https://hypersend.co.mz/api/me
```

### Response Structure

For successful retrieval of user profile, the response structure is:

```json
{
  "success": true,
  "data": {
    "user": {
      "id": 1,
      "name": "User Example",
      "email": "user@example.com",
      "email_verified_at": null,
      "two_factor_confirmed_at": null,
      "current_team_id": null,
      "profile_photo_path": null,
      "created_at": "2023-08-02T10:12:00.000000Z",
      "updated_at": "2023-08-02T10:12:00.000000Z",
      "profile_photo_url": ""
    }
  }
}
```

For unsuccessful retrieval, the response structure is similar to the unsuccessful login response.
