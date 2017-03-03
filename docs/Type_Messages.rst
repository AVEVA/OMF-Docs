===============
 Type Messages
===============
Types are defined using the JSON Schema specification (http://json-schema.org/). For details on supported property data types and formats, see :doc:`Property_Types_and_Formats`.

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
=================== =============================

The ``id`` cannot begin with the character sequence __. This is reserved for predefined Types. Currently supported predefined Types are __Link and __Span.

A ``static`` classification represents metadata describing a device being observed and should be used to capture data that is descriptive and relatively unchanging. A ``dynamic`` classification represents observed or calculated measurements taken from a device.

One property must be designated as the index by supplying the ``index`` keyword with a value of ``true``. The designated ``index`` property is used to uniquely identify discrete Data objects so that they can be updated or deleted after their initial creation.

One property may be optionally designated as the name by supplying the ``name`` keyword with a value of ``true``. If no property is declared to be the ``name``, the property marked as the ``index`` will be used as the name. Because the ``index`` must be unique across all assets, the name keyword allows for multiple distinct Data objects to share a common name.


.. toctree::

   Link_Type
   Span_Type 
   Property_Types_and_Formats
   Type_Msg_Sample
