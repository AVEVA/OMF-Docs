Container Messages
------------------

A Container can be defined for Type defintions whose classification is ``dynamic``, and provides a collection of Streams for Type properties. Each Container has a unique ID, defined upon creation of the Container.

Once a Type has been registered with a Type message, Containers can begin using that Type. Containers can be created, updated, or deleted.

The body of a Container message consists of an array of objects with the following keywords:

=======================	==================================================================================
Name					Value
=======================	==================================================================================
``id``          		Unique identifier of the Container.
``typeid``        		ID of the Type used by the Container.
``typeversion`` 		Optional version of the Type used by the Container. The version must be of format x.x.x.x, where x must be an integer greater than or equal to 0. If omitted, version 1.0.0.0 is used.
``name`` 	    		Optional friendly name for the Container.
``description`` 		Optional description for the Container.
``tags``        		Optional array of strings to tag the Container.
``metadata``    		Optional key-value pairs associated with the Container. A predefined metadata key is ``datasource``.
``indexes``     		Optional array of Type Property ids to be used as secondary indexes for the Container.
``propertyoverrides``	Optional key-value pairs used to override properties on a Type definition. 
=======================	==================================================================================

When using the ``propertyoverrides`` keyword, the format of the value should follow the format of the ``properties`` defined on the Type. Currently supported overrides include ``name``, ``description``, ``uom``, ``minimum``, and ``maximum``. 
Refer to the :doc:`Type Properties and Formats <Type_Properties_and_Formats>` for a complete list of Type ``properties``. 

``metadata`` is used to associate property values with properties on a Stream. Specify the source of a stream of data using the ``datasource`` keyword within the ``metadata``, for example: 

::

	{ "metadata": { "datasource": "OPCUA" } }


.. toctree::

      Container_Msg_Sample
