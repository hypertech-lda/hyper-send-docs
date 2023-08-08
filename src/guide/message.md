# SMS through API

The SMS API provides functionality to manage customer massages. You can perform various actions, such as listing all massages or retrieving specific contact details. The API follows RESTful conventions and offers the following endpoints:

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

Certainly! Here's the Markdown for sending messages with the provided parameters:

## Send SMS Message

To send an SMS message to multiple contacts, use a POST request to the following URL:

```txt
https://hypersend.co.mz/api/send-sms
```

### Request Body

To schedule an SMS message for future delivery, include the optional `scheduled_to` parameter in your request. This parameter allows you to specify the date and time when you want the message to be sent. If the `scheduled_to` parameter is not provided, the message will be sent immediately upon submission.

| Key          | Description                                      | Required | Example                 |
| ------------ | ------------------------------------------------ | -------- | ----------------------- |
| message      | The text of the SMS message                      | Yes      | "Hello from HyperSend!" |
| contacts     | An array of contact numbers (min 10 digits)      | Yes      | ["+2588xxxxxxx", ...]   |
| template_id  | ID of a predefined message template (optional)   | No       | 123                     |
| scheduled_to | Date and time to schedule the message (optional) | No       | "2023-08-10 15:00:00"   |

#### Example JSON object for immediate delivery (without scheduling):

```json
{
  "message": "Hello from HyperSend!",
  "contacts": ["+2588xxxxxxx", "+2588yyyyyyy"],
}
```

#### Example JSON object for scheduled delivery (with `scheduled_to` parameter):

```json
{
  "message": "Hello from HyperSend!",
  "contacts": ["+2588xxxxxxx", "+2588yyyyyyy"],
  "scheduled_to": "2023-08-10 15:00:00"
}
```

Remember to format the `scheduled_to` parameter as "YYYY-MM-DD HH:MM:SS" to ensure accurate scheduling.

### Response Structure

For a successful message submission, the response structure is:

```json
{
  "success": true,
  "message": "Message sent successfully",
  "data": {
    "messages": [{
       "id": 1,
        "contact_group_id": null,
        "message_tamplete_id": null,
        "uuid": "d01ac9da-2ef9-4647-9c86-12d182ca215b",
        "message": "Hello from HyperSend!",
        "nr_sms": 1,
        "lenght": 9,
        "per_message": 9,
        "scheduled_to": "2023-08-02 12:18:22",
        "sent_at": null,
        "phone": "+2588xxxxxxx",
        "dail_code": "258",
        "status": "sent",
        "created_at": "2023-08-02T10:18:22.000000Z",
        "updated_at": "2023-08-02T10:18:44.000000Z",
    },
    {
       "id": 2,
        "contact_group_id": null,
        "message_tamplete_id": null,
        "uuid": "d01ac9da-2ef9-4647-9c86-12d182ca215b",
        "message": "Hello from HyperSend!",
        "nr_sms": 1,
        "lenght": 9,
        "per_message": 9,
        "scheduled_to": "2023-08-02 12:18:22",
        "sent_at": null,
        "phone": "+2588yyyyyyy",
        "dail_code": "258",
        "status": "sent",
        "created_at": "2023-08-02T10:18:22.000000Z",
        "updated_at": "2023-08-02T10:18:44.000000Z",
    }]
  }
}
```

For unsuccessful message submission, the response structure is similar to other error responses.

### Note

- The `contacts` array should contain valid contact numbers, each starting with a "+". Minimum 10 digits are required for each contact.
- You can provide a `template_id` to use a predefined message template.
- Use `scheduled_to` to schedule a message for a future date and time.



<br>
<hr>

## List all messages

To list messages, send GET request to following URL:

```txt
https://hypersend.co.mz/api/messages
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
    "messages": [
      {
       "id": 1,
        "contact_group_id": null,
        "message_tamplete_id": null,
        "uuid": "d01ac9da-2ef9-4647-9c86-12d182ca215b",
        "message": "Hello from HyperSend!",
        "nr_sms": 1,
        "lenght": 9,
        "per_message": 9,
        "scheduled_to": "2023-08-02 12:18:22",
        "sent_at": null,
        "phone": "+2588xxxxxxx",
        "dail_code": "258",
        "status": "sent",
        "created_at": "2023-08-02T10:18:22.000000Z",
        "updated_at": "2023-08-02T10:18:44.000000Z",
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
    "messages": {
      "current_page": 1,
      "data": [
        {
          "id": 1,
        "contact_group_id": null,
        "message_tamplete_id": null,
        "uuid": "d01ac9da-2ef9-4647-9c86-12d182ca215b",
        "message": "Hello from HyperSend!",
        "nr_sms": 1,
        "lenght": 9,
        "per_message": 9,
        "scheduled_to": "2023-08-02 12:18:22",
        "sent_at": null,
        "phone": "+2588xxxxxxx",
        "dail_code": "258",
        "status": "sent",
        "created_at": "2023-08-02T10:18:22.000000Z",
        "updated_at": "2023-08-02T10:18:44.000000Z",
        }
      ],
      "first_page_url": "https://hypersend.co.mz/api/messages?page=1",
      "from": 1,
      "last_page": 10,
      "last_page_url": "https://hypersend.co.mz/api/messages?page=10",
      "links": [
        {
          "url": null,
          "label": "&laquo; Anterior",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/messages?page=1",
          "label": "1",
          "active": true
        },
        {
          "url": "https://hypersend.co.mz/api/messages?page=2",
          "label": "2",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/messages?page=3",
          "label": "3",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/messages?page=4",
          "label": "4",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/messages?page=5",
          "label": "5",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/messages?page=6",
          "label": "6",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/messages?page=7",
          "label": "7",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/messages?page=8",
          "label": "8",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/messages?page=9",
          "label": "9",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/messages?page=10",
          "label": "10",
          "active": false
        },
        {
          "url": "https://hypersend.co.mz/api/messages?page=2",
          "label": "Próximo &raquo;",
          "active": false
        }
      ],
      "next_page_url": "https://hypersend.co.mz/api/messages?page=2",
      "path": "https://hypersend.co.mz/api/messages",
      "per_page": 1,
      "prev_page_url": null,
      "to": 1,
      "total": 10
    }
  }
}
```

## Show message

To retrieve a specific message, send a GET request to the following URL:

```txt
https://hypersend.co.mz/api/messages/{message_id}
```

Replace `{message_id}` with the actual ID of the message you want to retrieve.

### Response Structure

Here is an example of a success response for showing a message:

```json
{
  "success": true,
  "data": {
    "message": {
      "id": 1,
        "contact_group_id": null,
        "message_tamplete_id": null,
        "uuid": "d01ac9da-2ef9-4647-9c86-12d182ca215b",
        "message": "Hello from HyperSend!",
        "nr_sms": 1,
        "lenght": 9,
        "per_message": 9,
        "scheduled_to": "2023-08-02 12:18:22",
        "sent_at": null,
        "phone": "+2588xxxxxxx",
        "dail_code": "258",
        "status": "sent",
        "created_at": "2023-08-02T10:18:22.000000Z",
        "updated_at": "2023-08-02T10:18:44.000000Z",
    }
  }
}
```


## Delete message

To delete a message, send a DELETE request to the following URL:

```txt
https://hypersend.co.mz/api/messages/{message_id}
```

Replace `{message_id}` with the actual ID of the message you want to delete.

### Response Structure

Here is an example of a success response after deleting a message:

```json
{
  "success": true,
  "message": "Message deleted successfully"
}
}
```
