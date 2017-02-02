===============
 Type Messages
===============
Types are defined using the JSON Schema specification (http://json-schema.org/). For details on supported property data types and formats, see :doc:`Property_Types_and_Formats`.

Types can be created, updated, or deleted. Updating a Type without updating the Type’s version will result in failure. Once a Type is deleted, any operations on Groups or Data using that Type will fail.

The body of a Group message consists of an array of objects. The following keywords are used to define a Type:

=================== =============================
Name                Value
=================== =============================
``id``   	        Unique identifier of the Type.
``classification``  One of ``value``, ``link``, or ``span``. Specifies the Data this Type can define. Optional: defaults to ``value``.
``version``         Optional version of the Type used by the Group. If omitted version 1.0.0.0 is assumed.
``name``            Optional friendly name for the Type.
``description``     Optional description for the Type.
``tags``            Optional array of strings to tag the Type.
``metadata``        Optional key-value pairs associated with the Type.
=================== =============================

One property must be designated as the index by supplying the ``index`` keyword with a value of ``true``. The designated index property is used to uniquely identify discrete Data objects so that they can be updated or deleted after their initial creation.

Depending on the Type’s classification, additional properties are required.


.. toctree::

   Span_Types
   Link_Types
   Property_Types_and_Formats
   Type_Msg_Sample
