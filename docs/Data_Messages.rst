Data Messages
-------------

Data messages can span multiple Types and Groups. The body of a Data message is composed of an array of objects with the following properties: 

=============== =================================================================================================
Name            Value
=============== =================================================================================================
``type``        Optional ID of the type. If omitted, group is expected.
``group``       Optional ID of the group. If omitted, type is expected.
``typeversion`` Optional version of the Type, if one is specified. If omitted, version 1.0.0.0 is assumed.
``values`` 	    An array of objects conforming to the type.
=============== =================================================================================================

For each object, either Type or Group must be specified. If a Group is specified, the values must conform to the Type with which the Group is associated. If a Type is specified, the values must conform to that Type.

.. toctree::

   Link_Data
   Span_Data
   Data_Msg_Sample
