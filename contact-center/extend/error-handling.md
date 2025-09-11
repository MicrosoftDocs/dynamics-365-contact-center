---
title: Error handling in messaging APIs
description: Learn how error handling in Dynamics 365 Customer Service and Dynamics 365 Contact Center messaging APIs works.
ms.date: 09/10/2025
ms.topic: how-to
author: gandhamm
ms.author: mgandham
ms.reviewer: mgandham
ms.custom: bap-template
---

# Error handling in messaging APIs

When you work with the Messaging APIs, it’s important to understand how errors are communicated as it helps you implement proper error handling and debugging in your applications.

The APIs return standard HTTP status codes to indicate success or failure, and includes detailed error messages in the response body. These error responses often follow the [RFC 7807](https://datatracker.ietf.org/doc/html/rfc7807) specification for problem details in HTTP APIs.

In addition to the status code and message, failed requests include a correlation ID in the response headers that you can use for troubleshooting.


## HTTP Status Codes

| Status Code | Meaning             | Description |
|-------------|---------------------|-------------|
| 400       | Bad Request          | The request didn't conform to the API contract. The response follows [RFC 7807 Problem Details](https://datatracker.ietf.org/doc/html/rfc7807). |
| 401       | Unauthorized         | The token is expired, invalid, or the channel ID isn't authorized for the organization. |
| 404       | Not Found            | The specified conversation ID wasn't found or is already closed. |
| 429       | Too Many Requests    | The request rate limit has exceeded. The `Retry-After` header indicates when you can retry. |
| 500       | Internal Server Error| The omnichannel service failed to process the request. |
| 503       | Service Unavailable  | The omnichannel service is temporarily unavailable. |



### Sample 400 Error (RFC 7807 Format)

```json
{
  "type": "https://en.wikipedia.org/wiki/Square_root",
  "title": "Bad Input",
  "status": 400,
  "detail": "Negative or complex numbers are not allowed."
}

```

## Error codes in response body

| Error Code | Error Message                                                               | HTTP Code |
| ---------- | --------------------------------------------------------------------------- | --------- |
| 30001    | The provided organization ID isn't valid.                                  | 400     |
| 30002    | The provided channel ID isn't valid.                                       | 400     |
| 30003    | The requested operation is invalid or not supported.                        | 400     |
| 30004    | The specified channel configuration doesn't exist.                         | 404     |
| 30005    | The provided conversation ID isn't valid.                                  | 400     |
| 30006    | The provided timestamp isn't valid.                                        | 400     |
| 30007    | The page size for conversations must either be null or between 1 and 250.   | 400     |
| 30008    | The page size for messages must either be null or between 1 and 100.        | 400     |
| 30009    | The provided continuation token is invalid. Use the same token as before.   | 400     |
| 30010    | The conversation context size is too large. Maximum allowed is 100 entries. | 400     |
| 30011    | The message text length is too large. Max 6,000 characters allowed.          | 400     |
| 30012    | The request body was either not provided or is malformed.                   | 400     |
| 30013    | The specified conversation doesn't exist.                                  | 404     |
| 30014    | The specified channel configuration isn't linked to a workstream.          | 400     |
| 30015    | The response body wasn't serialized successfully. Contact customer support for help.                               | 500     |
| 30016    | The message activity has no text or attachments.                                  | 400     |


## Use CorrelationID for troubleshooting

Each failed response includes a header, `x-ms-correlation-id: <GUID>`, which uniquely identifies the transaction within the system. You can save this ID and share it with Microsoft support if you need help with troubleshooting specific failures.
