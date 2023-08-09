# Groups through API

The Group API provides functionality to manage customer groups. You can perform various actions, such as listing all groups or retrieving specific group details. The API follows RESTful conventions and offers the following endpoints:

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

## List all groups

To list groups, send GET request to following URL:

```txt
https://hypersend.co.mz/api/groups
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
    "groups": [
      {
        "id": 1,
        "name": "My Group",
        "description": "My Description.",
        "created_at": "2023-08-04T08:20:01.000000Z",
        "updated_at": "2023-08-04T08:20:01.000000Z"
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
    "groups": {
      "current_page": 1,
      "data": [
        {
          "id": 1,
          "name": "My Group",
          "description": "My Description.",
          "created_at": "2023-08-04T08:20:01.000000Z",
          "updated_at": "2023-08-04T08:20:01.000000Z"
        }
      ],
      "first_page_url": "https://hypersend.co.mz/api/groups?page=1",
      "from": 1,
      "last_page": 10,
      "last_page_url": "https://hypersend.co.mz/api/groups?page=10",
      "links": [
        {
          "url": null,
          "label": "&laquo; Anterior",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/groups?page=1",
          "label": "1",
          "active": true
        },
        {
          "url": "https://hypersend.co.mz/api/groups?page=2",
          "label": "2",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/groups?page=3",
          "label": "3",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/groups?page=4",
          "label": "4",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/groups?page=5",
          "label": "5",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/groups?page=6",
          "label": "6",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/groups?page=7",
          "label": "7",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/groups?page=8",
          "label": "8",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/groups?page=9",
          "label": "9",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/groups?page=10",
          "label": "10",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/groups?page=2",
          "label": "Próximo &raquo;",
          "active": false
        }
      ],
      "next_page_url": "https://hypersend.co.mz/api/groups?page=2",
      "path": "https://hypersend.co.mz/api/groups",
      "per_page": 1,
      "prev_page_url": null,
      "to": 1,
      "total": 10
    }
  }
}
```

## Show Contact

To retrieve a specific group, send a GET request to the following URL:

```txt
https://hypersend.co.mz/api/groups/{group_id}
```

Replace `{group_id}` with the actual ID of the group you want to retrieve.

### Response Structure

Here is an example of a success response for showing a group:

```json
{
  "success": true,
  "data": {
    "group": {
      "name": "My Group",
      "description": "My Description.",
      "created_at": "2023-08-04T08:20:01.000000Z",
      "updated_at": "2023-08-04T08:20:01.000000Z"
    }
  }
}
```

## Store Contact

To create a new group, send a POST request to the following URL:

```txt
https://hypersend.co.mz/api/groups
```

### Request Body

| Key         | Description         | Required | Example          |
| ----------- | ------------------- | -------- | ---------------- |
| name        | Group's name        | Yes      | "Jane Smith"     |
| description | Group's description | No       | "My Description" |

Example JSON object for the request body:

```json
{
  "name": "My Group",
  "description": "My Description."
}
```

### Response Structure

Here is an example of a success response after storing a group:

```json
{
  "success": true,
  "message": "Contact created successfully",
  "data": {
    "group": {
      "name": "My Group",
      "description": "My Description.",
      "created_at": "2023-08-04T08:20:01.000000Z",
      "updated_at": "2023-08-04T08:20:01.000000Z"
    }
  }
}
```

## Update Contact

To update an existing group, send a PUT request to the following URL:

```txt
https://hypersend.co.mz/api/groups/{group_id}
```

Replace `{group_id}` with the actual ID of the group you want to update.

### Request Body

You can include any combination of the following fields in the request body:

| Key         | Description         | Required | Example          |
| ----------- | ------------------- | -------- | ---------------- |
| name        | Group's name        | no       | "Jane Smith"     |
| description | Group's Description | no       | "My Description" |

Example JSON object for the request body:

```json
{
  "name": "My Group",
  "description": "My Description."
}
```

### Response Structure

Here is an example of a success response after updating a group:

```json
{
  "success": true,
  "message": "Contact updated successfully",
  "data": {
    "group": {
      "name": "My Group",
      "description": "My Description.",
      "created_at": "2023-08-04T08:20:01.000000Z",
      "updated_at": "2023-08-04T08:20:01.000000Z"
    }
  }
}
```

## Delete Contact

To delete a group, send a DELETE request to the following URL:

```txt
https://hypersend.co.mz/api/groups/{group_id}
```

Replace `{group_id}` with the actual ID of the group you want to delete.

### Response Structure

Here is an example of a success response after deleting a group:

```json
{
  "success": true,
  "message": "Contact deleted successfully"
}
```
