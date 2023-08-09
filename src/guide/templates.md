# Templates through API

The Templates API provides functionality to manage customer templates. You can perform various actions, such as listing all templates or retrieving specific template details. The API follows RESTful conventions and offers the following endpoints:

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

## List all templates

To list templates, send GET request to following URL:

```txt
https://hypersend.co.mz/api/templates
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
    "templates": [
      {
        "id": 1,
        "name": "Template name",
        "header": "Template Header-container",
        "footer": "Template Footer-container",
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
    "templates": {
      "current_page": 1,
      "data": [
        {
          "id": 1,
          "name": "Template name",
          "header": "Template Header-container",
          "footer": "Template Footer-container",
          "created_at": "2023-08-02T10:18:14.000000Z",
          "updated_at": "2023-08-02T10:18:14.000000Z"
        }
      ],
      "first_page_url": "https://hypersend.co.mz/api/templates?page=1",
      "from": 1,
      "last_page": 10,
      "last_page_url": "https://hypersend.co.mz/api/templates?page=10",
      "links": [
        {
          "url": null,
          "label": "&laquo; Anterior",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/templates?page=1",
          "label": "1",
          "active": true
        },
        {
          "url": "https://hypersend.co.mz/api/templates?page=2",
          "label": "2",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/templates?page=3",
          "label": "3",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/templates?page=4",
          "label": "4",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/templates?page=5",
          "label": "5",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/templates?page=6",
          "label": "6",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/templates?page=7",
          "label": "7",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/templates?page=8",
          "label": "8",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/templates?page=9",
          "label": "9",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/templates?page=10",
          "label": "10",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/templates?page=2",
          "label": "Próximo &raquo;",
          "active": false
        }
      ],
      "next_page_url": "https://hypersend.co.mz/api/templates?page=2",
      "path": "https://hypersend.co.mz/api/templates",
      "per_page": 1,
      "prev_page_url": null,
      "to": 1,
      "total": 10
    }
  }
}
```

## Show Template

To retrieve a specific template, send a GET request to the following URL:

```txt
https://hypersend.co.mz/api/templates/{template_id}
```

Replace `{template_id}` with the actual ID of the template you want to retrieve.

### Response Structure

Here is an example of a success response for showing a template:

```json
{
  "success": true,
  "data": {
    "template": {
      "id": 1,
      "name": "Template name",
      "header": "Template Header-container",
      "footer": "Template Footer-container",
      "created_at": "2023-08-02T10:18:14.000000Z",
      "updated_at": "2023-08-02T10:18:14.000000Z"
    }
  }
}
```

## Store Template

To create a new template, send a POST request to the following URL:

```txt
https://hypersend.co.mz/api/templates
```

### Request Body

| Key    | Description       | Required | Example           |
| ------ | ----------------- | -------- | ----------------- |
| name   | Template's Name   | Yes      | "Template Name"   |
| header | Template's Header | Yes      | "Template Header" |
| footer | Template's Footer | Yes      | "Template Footer" |

Example JSON object for the request body:

```json
{
  "name": "Template Name",
  "header": "Template Header",
  "footer": "Template Footer"
}
```

### Response Structure

Here is an example of a success response after storing a template:

```json
{
  "success": true,
  "message": "Template created successfully",
  "data": {
    "template": {
      "id": 1,
      "name": "Template name",
      "header": "Template Header-container",
      "footer": "Template Footer-container",
      "created_at": "2023-08-02T10:18:14.000000Z",
      "updated_at": "2023-08-02T10:18:14.000000Z"
    }
  }
}
```

## Update Template

To update an existing template, send a PUT request to the following URL:

```txt
https://hypersend.co.mz/api/templates/{template_id}
```

Replace `{template_id}` with the actual ID of the template you want to update.

### Request Body

You can include any combination of the following fields in the request body:

| Key    | Description    | Required | Example           |
| ------ | -------------- | -------- | ----------------- |
| name   | Updated Name   | No       | "Template Name"   |
| header | Updated Header | No       | "Template Header" |
| footer | Updated Footer | No       | "Template Footer" |

Example JSON object for the request body:

```json
{
  "name": "Template Name",
  "header": "Template Header",
  "footer": "Template Footer"
}
```

### Response Structure

Here is an example of a success response after updating a template:

```json
{
  "success": true,
  "message": "Template updated successfully",
  "data": {
    "template": {
      "id": 1,
      "name": "Template name",
      "header": "Template Header-container",
      "footer": "Template Footer-container",
      "created_at": "2023-08-02T10:18:14.000000Z",
      "updated_at": "2023-08-02T10:18:14.000000Z"
    }
  }
}
```

## Delete Template

To delete a template, send a DELETE request to the following URL:

```txt
https://hypersend.co.mz/api/templates/{template_id}
```

Replace `{template_id}` with the actual ID of the template you want to delete.

### Response Structure

Here is an example of a success response after deleting a template:

```json
{
  "success": true,
  "message": "Template deleted successfully"
}
```
