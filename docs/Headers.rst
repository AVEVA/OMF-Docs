Headers
=======

The following headers are supported in version 1.1 of the message specification. Headers may 
be added or removed over time. Backwards compatibility is achievable through the ``omfversion`` header. 

=================    ========================================================================================
Name                 Value
=================    ========================================================================================
``producertoken``    A unique token used to identify and authorize a given OMF producer. Consult the OSIsoft 
                     Cloud Services or PI Connector Relay documentation for further information. 
``messagetype``      Describes the type of message contained in the message body. One of: 
                     ``type``, ``container``, or ``data``. See :doc:`Message_Types`.
``messageformat``    Describes the data serialization format employed in the message body. Currently 
                     limited to ``json``.
``omfversion``       Specifies the version of the OSIsoft Message Format used in the message. The version for the current specification is 1.1.
``action``           Optional: One of: ``create``, ``update``, or ``delete``. Describes the action to be 
                     performed using the data in the message body. If omitted, ``create`` is assumed.
``compression``	     Optional: The compression algorithm used to compress the message body. Currently 
                     limited to ``gzip``. If not specified, the message body is assumed to be uncompressed.
=================    ========================================================================================
