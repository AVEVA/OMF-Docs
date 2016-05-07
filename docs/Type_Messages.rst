Type Messages
-------------
Any type used by a stream must be registered before the stream can be created. Types can be created, updated, or deleted. Updating a type without updating the type's version will result in failure. Once a type is deleted, any operations on streams using that type will fail.

The body of a Type message consists of an array of JSON Schema formatted types, as described in :doc:`Types`.

.. toctree::

   Type_Msg_Sample
