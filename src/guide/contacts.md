# Contacts through API

The Contacts API provides functionality to manage customer contacts. You can perform various actions, such as listing all contacts or retrieving specific contact details. The API follows RESTful conventions and offers the following endpoints:


## Headers

To ensure proper authentication and communication, include the following headers in your API requests:

| Key           | Value                         |
| ------------- | ----------------------------- |
| Accept        | `application/json`            |
| Content-Type  | `application/json`            |
| Authorization | Bearer YOUR_ACCESS_TOKEN_HERE |

Replace `YOUR_ACCESS_TOKEN_HERE` with the actual bearer token you have obtained after successful authentication. This token will be used to authenticate your API requests and grant access to the protected endpoints.

### Additional information

The following additional information may be helpful:

- The HyperSend API uses the JSON format for all responses.
<!-- - The HyperSend API uses HTTP status codes to indicate the success or failure of a request. -->
- The HyperSend API uses the `success` property to indicate whether a request was successful.
- The HyperSend API uses the `message` property to provide additional information about the status of a response.
- The HyperSend API uses the `data` property to return data from a successful request.

### Response structure

The response structure for both error and success responses is the same:

```json
{
  "success": true|false,
  "message": "Response message"
  "data": {}
}
```

The `success` property indicates whether the request was successful. If the request was successful and the `message` property will be a success message. If the request was not successful, the `status` property will be an error code and the `message` property will be an error message.

The `data` property is only present in success responses. It contains the data that was returned by the API. The data structure will vary depending on the API endpoint that was called.

<br>
<hr>

## List all contacts

To list contacts, send GET request to following URL:

```txt
https://hypersend.co.mz/api/contacts
```

## Request Body

| Key      | Description                                     | Required | Example |
| -------- | ----------------------------------------------- | -------- | ------- |
| paginate | Set to a positive integer to enable pagination. | No       | 16      |

Example JSON object for the request body:

```json
{
  "paginate": 16
}
```

<!-- ![Request Payment Link](./images/api-url-request.png) -->

### Response structure

Here are some examples of error and success responses:

**Error response**

```json
{
  "success": false,
  "message": "Invalid paginate value"
}
```

**Success response without parameters**

```json
{
  "success": true,
  "data": {
    "contacts": [
      {
        "id": 1,
        "name": "My Contact",
        "iso2": "",
        "country_code": "MZ",
        "email": "exemplo@email.com",
        "country_name": "Mozambique (Moçambique)",
        "dial_code": "258",
        "formatted": "8x xxx xxx",
        "number": "+2588xxxxxxx",
        "national_number": "84xxxxxx",
        "created_at": "2023-08-02T10:18:14.000000Z",
        "updated_at": "2023-08-02T10:18:14.000000Z"
      }
    ]
  }
}
```

**Success response with paginate parameters**

```json
{
  "success": true,
  "data": {
    "contacts": {
      "current_page": 1,
      "data": [
        {
          "id": 1,
          "name": "My Contact",
          "iso2": "",
          "country_code": "MZ",
          "email": "exemplo@email.com",
          "country_name": "Mozambique (Moçambique)",
          "dial_code": "258",
          "formatted": "8x xxx xxx",
          "number": "+2588xxxxxxx",
          "national_number": "84xxxxxx",
          "created_at": "2023-08-02T10:18:14.000000Z",
          "updated_at": "2023-08-02T10:18:14.000000Z"
        }
      ],
      "first_page_url": "https://hypersend.co.mz/api/contacts?page=1",
      "from": 1,
      "last_page": 10,
      "last_page_url": "https://hypersend.co.mz/api/contacts?page=10",
      "links": [
        {
          "url": null,
          "label": "&laquo; Anterior",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/contacts?page=1",
          "label": "1",
          "active": true
        },
        {
          "url": "https://hypersend.co.mz/api/contacts?page=2",
          "label": "2",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/contacts?page=3",
          "label": "3",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/contacts?page=4",
          "label": "4",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/contacts?page=5",
          "label": "5",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/contacts?page=6",
          "label": "6",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/contacts?page=7",
          "label": "7",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/contacts?page=8",
          "label": "8",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/contacts?page=9",
          "label": "9",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/contacts?page=10",
          "label": "10",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/contacts?page=2",
          "label": "Próximo &raquo;",
          "active": false
        }
      ],
      "next_page_url": "https://hypersend.co.mz/api/contacts?page=2",
      "path": "https://hypersend.co.mz/api/contacts",
      "per_page": 1,
      "prev_page_url": null,
      "to": 1,
      "total": 10
    }
  }
}
```

## Show Contact

To retrieve a specific contact, send a GET request to the following URL:

```txt
https://hypersend.co.mz/api/contacts/{contact_id}
```

Replace `{contact_id}` with the actual ID of the contact you want to retrieve.

### Response Structure

Here is an example of a success response for showing a contact:

```json
{
  "success": true,
  "data": {
    "contact": {
      "id": 1,
      "name": "My Contact",
      "iso2": "",
      "country_code": "MZ",
      "email": "exemplo@email.com",
      "country_name": "Mozambique (Moçambique)",
      "dial_code": "258",
      "formatted": "8x xxx xxx",
      "number": "+2588xxxxxxx",
      "national_number": "84xxxxxx",
      "created_at": "2023-08-02T10:18:14.000000Z",
      "updated_at": "2023-08-02T10:18:14.000000Z"
    }
  }
}
```

## Store Contact

To create a new contact, send a POST request to the following URL:

```txt
https://hypersend.co.mz/api/contacts
```

### Request Body

| Key   | Description                            | Required | Example            |
| ----- | -------------------------------------- | -------- | ------------------ |
| phone | Contact's phone number (starts with +) | Yes      | "+123456789"       |
| name  | Contact's name                         | Yes      | "Jane Smith"       |
| email | Contact's email                        | No       | "jane@example.com" |

Example JSON object for the request body:

```json
{
  "phone": "+123456789",
  "name": "Jane Smith",
  "email": "jane@example.com"
}
```

### Response Structure

Here is an example of a success response after storing a contact:

```json
{
  "success": true,
  "message": "Contact created successfully",
  "data": {
    "contact": {
      "id": 2,
      "name": "Jane Smith",
      "iso2": "",
      "country_code": "USA",
      "email": "jane@example.com",
      "country_name": "Mozambique (Moçambique)",
      "dial_code": "258",
      "formatted": "1 234 56 789",
      "number": "+123456789",
      "national_number": "123456789",
      "created_at": "2023-08-02T10:18:14.000000Z",
      "updated_at": "2023-08-02T10:18:14.000000Z"
    }
  }
}
```

## Update Contact

To update an existing contact, send a PUT request to the following URL:

```txt
https://hypersend.co.mz/api/contacts/{contact_id}
```

Replace `{contact_id}` with the actual ID of the contact you want to update.

### Request Body

You can include any combination of the following fields in the request body:

| Key   | Description                          | Required | Example               |
| ----- | ------------------------------------ | -------- | --------------------- |
| phone | Updated phone number (starts with +) | No       | "+987654321"          |
| name  | Updated name                         | No       | "Updated Name"        |
| email | Updated email                        | No       | "updated@example.com" |

Example JSON object for the request body:

```json
{
  "phone": "+987654321",
  "name": "Updated Name"
}
```

### Response Structure

Here is an example of a success response after updating a contact:

```json
{
  "success": true,
  "message": "Contact updated successfully",
  "data": {
    "contact": {
      "id": 2,
      "name": "Updated Name",
      "iso2": "",
      "country_code": "MZ",
      "email": "jane@example.com",
      "country_name": "Mozambique (Moçambique)",
      "dial_code": "258",
      "formatted": "98 765 4321",
      "number": "+987654321",
      "national_number": "987654321",
      "created_at": "2023-08-02T10:18:14.000000Z",
      "updated_at": "2023-08-02T10:18:14.000000Z"
    }
  }
}
```

## Delete Contact

To delete a contact, send a DELETE request to the following URL:

```txt
https://hypersend.co.mz/api/contacts/{contact_id}
```

Replace `{contact_id}` with the actual ID of the contact you want to delete.

### Response Structure

Here is an example of a success response after deleting a contact:

```json
{
  "success": true,
  "message": "Contact deleted successfully"
}
```
