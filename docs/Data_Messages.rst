Data Messages
-------------

Data messages can span multiple Types and Containers. The body of a Data message is composed of a JSON array with JSON objects defined by the following keywords: 

=============== =================================================================================================
Name            Value
=============== =================================================================================================
``typeid``      Optional ID of the type. If omitted, container is expected.
``containerid`` Optional ID of the container. If omitted, type is expected.
``typeversion`` Optional version of the Type, if one is specified. The version must be of format x.x.x.x, where x must be an integer greater than or equal to 0. If omitted, version 1.0.0.0 is assumed.
``values`` 	    An array of objects conforming to the type.
=============== =================================================================================================

For each object, either ``typeid`` or ``containerid`` must be specified. If ``containerid`` is specified, the values must conform to the Type with which the Container is associated. If ``typeid`` is specified, the values must conform to that Type.

If a Type Property is defined but no property value is provided in the Data message, a default value will be assumed. Default values are specified in :doc:`Type_Properties_and_Formats`.


   
Linking instances of Types and Containers using Data messages:

``__Link`` messages are used to create relationships between instances of types, or instances of a type and container. To define a link relationship, set the ``typeid`` of the data message to ``__Link``. 
In the ``values`` array, define the ``source`` and ``target`` of the link relationship using the format defined by :doc:`Link Type<Link_Type>`


For examples of Linking Data, and examples of Data Messages see the following Topics:

.. toctree::

	Link_Type   	
	Data_Msg_Sample
