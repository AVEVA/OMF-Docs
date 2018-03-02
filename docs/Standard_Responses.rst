HTTP Status Codes
=================

The following status codes are returned by OSIsoft products accepting OMF messages over HTTP.

============================= =============================
Status code                   Description
============================= =============================
``204 No Content``   	      OMF message was successfully processed.
``400 Bad request``           The OMF message was malformed or not understood. The client should not retry sending the message without modifications.
``401 Anauthorized``          Authentication failed.
``403 Forbidden``             Authentication succeeded, but not authorized.
``413 Payload Too Large``     Payload size exceeds OMF body size limit.
``500 Internal Server Error`` The server encountered an unexpected condition.
``503 Service Unavailable``   The server is currently unavailable, retry later.
============================= =============================