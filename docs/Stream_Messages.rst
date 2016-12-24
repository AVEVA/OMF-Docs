Stream Messages
---------------

A Stream is defined as a sequence of data events of identical type, where each event has a unique, definable index. Each Stream has a unique ID, defined upon creation of the Stream.

Streams are designed to represent observed or calculated measurements taken from devices. Stream definition messages sent to an on-premises PI system must define an index property of timestamp type. Each additional property of the object is then mapped to a PI point. As Data messages associated with the Stream are sent to the system, they are timestamped using the index property.

When sending Data messages to a cloud-hosted Qi system, the index attribute may be of any type. Each attribute defined in the stream type is collated into a single Qi stream, rather than split into multiple streams or points.
  
Once a Type has been registered with a Type message, Streams can begin using that Type. Streams can be created, updated, or deleted.

The body of a Stream message consists of an array of objects made up of the following properties:

=============== =================================================================================================
Name            Value
=============== =================================================================================================
``id``          Unique identifier of the stream.
``type``        ID of the type used by the stream.
``typeVersion`` Optional version of the type used by the stream. If omitted, the highest version sent is assumed.
=============== =================================================================================================

.. toctree::

      Stream_Msg_Sample
