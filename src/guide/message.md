# SMS through API

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

Certainly! Here's the Markdown for sending messages with the provided parameters:

## Send SMS Message

To send an SMS message to multiple contacts, use a POST request to the following URL:

```txt
https://hypersend.co.mz/api/send-sms
```

### Request Body

| Key         | Description                                        | Required | Example                   |
| ----------- | -------------------------------------------------- | -------- | ------------------------- |
| message     | The text of the SMS message                        | Yes      | "Hello from HyperSend!"   |
| contacts    | An array of contact numbers (min 10 digits)       | Yes      | ["+2588xxxxxxx", ...]     |
| template_id | ID of a predefined message template (optional)     | No       | 123                       |
| scheduled_to| Date and time to schedule the message (optional)  | No       | "2023-08-10 15:00:00"     |

Example JSON object for the request body:

```json
{
  "message": "Hello from HyperSend!",
  "contacts": ["+2588xxxxxxx", "+2588yyyyyyy"],
  "template_id": 123,
  "scheduled_to": "2023-08-10 15:00:00"
}
```

### Response Structure

For a successful message submission, the response structure is:

```json
{
  "success": true,
  "message": "Message sent successfully",
  "data": {
    "message": {
      "id": 1,
      "text": "Hello from HyperSend!",
      "status": "queued",
      "scheduled_at": "2023-08-10 15:00:00",
      "created_at": "2023-08-07T10:00:00.000000Z",
      "updated_at": "2023-08-07T10:00:00.000000Z"
    }
  }
}
```

For unsuccessful message submission, the response structure is similar to other error responses.

### Note

- The `contacts` array should contain valid contact numbers, each starting with a "+". Minimum 10 digits are required for each contact.
- You can provide a `template_id` to use a predefined message template.
- Use `scheduled_to` to schedule a message for a future date and time.

Feel free to customize and expand upon this documentation as needed for your messaging platform. If you have further questions or need assistance, please let me know!