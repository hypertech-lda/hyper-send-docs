# Contacts through API

The Contacts API allows you to manage contacts for a customer. You can perform various operations such as listing all contacts or retrieving a specific contact. The API follows RESTful conventions and supports the following endpoints:

## Headers
Sure, I will add the "Authorization" header with the Bearer token to the existing headers:

| Key              | Value                                    |
| ---------------- | ---------------------------------------- |
| Accept           | `application/json`                       |
| Content-Type     | `application/json`                       |
| Authorization    | Bearer YOUR_ACCESS_TOKEN_HERE            |

Replace `YOUR_ACCESS_TOKEN_HERE` with the actual bearer token you have obtained after successful authentication. This token will be used to authenticate your API requests and grant access to the protected endpoints.


### Additional information

The following additional information may be helpful:

- The HyperSend API uses the JSON format for all responses.
- The HyperSend API uses HTTP status codes to indicate the success or failure of a request.
- The HyperSend API uses the `success` property to indicate whether a request was successful.
- The HyperSend API uses the `message` property to provide additional information about the status of a response.
- The HyperSend API uses the `data` property to return data from a successful request.

### Response structure

The response structure for both error and success responses is the same:

```json
{
  "success": true|false,
  "message": "Response error message"
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

| Key                | Description                                                                             | Required | Example                                          |
| ------------------ | --------------------------------------------------------------------------------------- | -------- | ------------------------------------------------ |
| paginate        | Set to a positive integer to enable pagination.                            | No      | 16                         |


Example JSON object for the request body:

```json
{
  "paginate": 16,
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
        "name": "Meu contacto",
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
        "name": "Meu contacto",
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
