Data Messages
-------------

Data messages can span multiple Types and Containers. The body of a Data message is composed of an array of objects with the following keywords: 

=============== =================================================================================================
Name            Value
=============== =================================================================================================
``typeid``      Optional ID of the type. If omitted, container is expected.
``containerid`` Optional ID of the container. If omitted, type is expected.
``typeversion`` Optional version of the Type, if one is specified. If omitted, version 1.0.0.0 is assumed.
``values`` 	    An array of objects conforming to the type.
=============== =================================================================================================

For each object, either ``typeid`` or ``containerid`` must be specified. If ``containerid`` is specified, the values must conform to the Type with which the Container is associated. If ``typeid`` is specified, the values must conform to that Type.

If a Type Property is defined but no property value is provided in the Data message, a default value will be assumed. Default values are specified in :doc:`Property_Types_and_Formats`.

.. toctree::

   Data_Msg_Sample
