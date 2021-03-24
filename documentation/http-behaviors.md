---
uid: http-behaviors
---

# Http Behaviors

While the OMF specification does not define a particular binary message protocol, OSIsoft systems accepting OMF over HTTP conform to a set of behaviors described in this section.
## Message Size

The body of an OMF message has a maximum size of 192KB. A request with a body size exceeding the maximum will be rejected with an HTTP response code 
of `413 Payload Too Large`. Compression is highly recommended for optimal performance.

## HTTP Status Codes

The following status codes are returned by OSIsoft products accepting OMF messages over HTTP.

| Status code | Description |
| --- | --- |
| `200 OK` | The OMF message was successfully processed. Response body contains additional information. |
| `202 Accepted` | The OMF message was received and has been successfully queued to be processed. |
| `204 No Content` | The OMF message was successfully processed, but there is no additional information to return. |
| `400 Bad Request` | The OMF message was malformed or not understood. The client should not retry sending the message without modifications. |
| `401 Unauthorized` | Authentication failed. |
| `403 Forbidden` | Authentication succeeded, but not authorized. |
| `413 Payload Too Large` | Payload size exceeds OMF body size limit. |
| `500 Internal Server Error` | The server encountered an unexpected condition. |
| `503 Service Unavailable` | The server is currently unavailable, retry later. |