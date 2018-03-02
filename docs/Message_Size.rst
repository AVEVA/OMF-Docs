Message Size
============

The body of an OMF message has a maximum size of 192KB. A request with a body size exceeding the maximum will be rejected with an HTTP response code of ``413 Payload Too Large``. Compression is highly recommended for optimal performance.