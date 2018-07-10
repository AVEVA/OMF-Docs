===============
 Type Messages
===============
Types are defined using the JSON Schema specification (http://json-schema.org/). For details on supported property data types and formats, see :doc:`Type_Properties_and_Formats`.

Types can be created, updated, or deleted. Updating a Type without updating the Type’s version will result in a failure. Once a Type is deleted, any operations on Containers or Data using that Type will fail.

The body of a Type message consists of an array of objects. The following keywords are used to define a Type:

=================== =============================
Name                Value
=================== =============================
``classification``  One of ``dynamic`` or ``static``.
``id``   	        Unique identifier of the Type.
``properties``      Key-value pairs defining the properties of the Type.
``type``            Inherited from JSON Schema. Must be set to ``object``.
``action``          Optional: One of: ``create``, ``update``, or ``delete``. The value specified overrides the value of the ``action`` header. If omitted, the value of the ``action`` header is assumed. See :doc:`Headers`.
``description``     Optional description for the Type.
``metadata``        Optional key-value pairs associated with the Type.
``name``            Optional friendly name for the Type.
``tags``            Optional array of strings to tag the Type.
``version``         Optional version of the Type. The version must be of format x.x.x.x, where x must be a positive integer.If omitted version 1.0.0.0 is assumed.
=================== =============================

The ``id`` cannot begin with the character sequence __. This is reserved for predefined Types. One currently supported predefined Type is __Link.

A ``static`` classification represents metadata describing a device being observed and should be used to capture data that is descriptive and relatively unchanging. A ``dynamic`` classification represents observed or calculated measurements taken from a device.


.. toctree::

   Link_Type
   Type_Properties_and_Formats
   Type_Msg_Sample
