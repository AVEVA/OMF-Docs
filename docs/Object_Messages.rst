Object Messages
---------------

Objects describe structural and relational data, as well as discrete events which are not associated with a continuous stream. Assets, Links, and Spans are all considered Objects.

.. toctree::
   Assets
   Links
   Spans

Objects must conform to a pre-defined Stream, Asset, Span, or Link type. On-premises systems translate Asset objects to AF elements, and Span objects to Event Frames. Link objects generate relationships between AF elements, PI data references, and Event Frames.

Once a type has been registered, object messages can be sent which use that type. Objects can be created, updated, or deleted.

The body of an Object message consists of an array of objects made up of the following properties:

=============== ========================================================================================
Name            Value
=============== ========================================================================================
``type``        ID of the type used by the object.
``typeVersion`` Optional version of the type. If omitted, the highest version sent is assumed.
``values``      An array of objects conforming to the type and typeVersion.
=============== ========================================================================================

.. toctree::

   Object_Msg_Sample
