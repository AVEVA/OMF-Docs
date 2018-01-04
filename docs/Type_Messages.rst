===============
 Type Messages
===============
Types are defined using the JSON Schema specification (http://json-schema.org/). For details on supported property data types and formats, see :doc:`Type_Properties_and_Formats`.

Types can be created, updated, or deleted. Updating a Type without updating the Type’s version will result in failure. Once a Type is deleted, any operations on Containers or Data using that Type will fail.

The body of a Type message consists of an array of objects. The following keywords are used to define a Type:

=================== =============================
Name                Value
=================== =============================
``id``   	        Unique identifier of the Type.
``classification``  One of ``dynamic`` or ``static``.
``version``         Optional version of the Type. If omitted version 1.0.0.0 is assumed.
``name``            Optional friendly name for the Type.
``description``     Optional description for the Type.
``tags``            Optional array of strings to tag the Type.
``metadata``        Optional key-value pairs associated with the Type.
``properties``      Key-value pairs defining the properties of the Type.
``type``            Inherited from JSON Schema. Must be set to ``object``.
=================== =============================

The ``id`` cannot begin with the character sequence __. This is reserved for predefined Types. One currently supported predefined Type is __Link.

A ``static`` classification represents metadata describing a device being observed and should be used to capture data that is descriptive and relatively unchanging. A ``dynamic`` classification represents observed or calculated measurements taken from a device.

.. toctree::

   Link_Type
   Type_Properties_and_Formats
   Type_Msg_Sample
