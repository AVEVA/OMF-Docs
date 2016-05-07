Stream Messages
---------------

Once a type has been registered, streams can begin using that type. Streams can be created, updated, or deleted.

The body of a Stream message consists of an array of objects made up of the following properties:

=============== =====================================================================================
Name            Value
=============== =====================================================================================
``streamId``    Unique identifier of the stream.
``typeId``      ID of the type used by the stream.
``typeVersion`` Optional version of the data type used by the stream. If omitted, 1.0.0.0 is assumed.
=============== =====================================================================================

.. toctree::

   Stream_Msg_Sample