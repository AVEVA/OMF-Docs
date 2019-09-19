===============
 Type Messages
===============
Types can be created, updated, or deleted. Updating a Type without updating the Type’s version will result in a failure. Once a Type is deleted, any operations on Containers or Data using that Type will fail.

The body of a Type message consists of an array of objects. The following keywords are used to define a Type:

=================== =============================
Name                Value
=================== =============================
``id``   	        Unique identifier of the Type.
``classification``  One of ``dynamic`` or ``static``.
``type``            Inherited from JSON Schema. Must be set to ``object``.
``version``         Optional version of the Type. The version must be of format x.x.x.x, where x must be an integer greater than or equal to 0. If omitted version 1.0.0.0 is assumed.
``name``            Optional friendly name for the Type.
``description``     Optional description for the Type.
``tags``            Optional array of strings to tag the Type.
``metadata``        Optional key-value pairs associated with the Type.
``enum``			Optional array of name/value pairs that define an enumeration set for properties that have a limited set of possible values. 
``properties``      \*Key-value pairs defining the properties of the Type. Required unless the Type definition contains ``enum``.
=================== =============================

\*When creating a Type message, the ``properties`` collection is required unless the Type is used to define an Enumeration set. In that case, the ``enum`` array will contain the required values.

The ``id`` cannot begin with the character sequence __. This has been reserved for predefined message definitions. Currently the only supported predefined Type is ``__Link``.
The ``id`` property is referenced when creating and linking ``types``, ``containers`` and ``data``.   

The format of the ``properties`` collection and allowed data types are defined in the :doc:`Type Properties and Formats <Type_Properties_and_Formats>` Topic.

A ``static`` classification represents metadata describing a device being observed and should be used to capture data that is descriptive and relatively unchanging.
A ``dynamic`` classification represents observed or calculated measurements taken from a device. 
For complex types that contain both ``static`` and ``dynamic`` data, use the :doc:`reftype <Type_Properties_and_Formats>` keyword in the ``properties`` definition to relate data. This provides support for Type reuse and inheritance of Type definitions.

An ``enum`` array defines an allowed set of name/value pairs and is used for properties that have a predefined set of values. Create the enum type separately from the definition of properties of that Type.
Refer to the :doc:`Enum <Enum_Type>` Topic for detailed information on defining an enumeration set.

	
For examples of Type messages and formatting refer to the following Topics:

.. toctree::

	Type_Properties_and_Formats	
	ComplexType_Msg_Sample
	Inheritance_Msg_Sample	
	Enum_Type	
