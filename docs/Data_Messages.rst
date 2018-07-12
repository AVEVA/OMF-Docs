Data Messages
-------------

Data messages can span multiple Types and Containers. Data can be created, updated, or deleted.

The body of a Data message is composed of an array of objects with the following keywords: 

=============== =================================================================================================
Name            Value
=============== =================================================================================================
``values`` 	    An array of objects conforming to the type.
``action``      Optional: One of: ``create``, ``update``, or ``delete``. The value specified overrides the value of the ``action`` header. If omitted, the value of the ``action`` header is assumed. See :doc:`Headers`.
``containerid`` Optional ID of the container. If omitted, type is expected.
``patch``		Optional array of properties to update. If specified, ``action`` must also be specified and set to ``update``.
``typeid``      Optional ID of the type. If omitted, container is expected.
``typeversion`` Optional version of the Type, if one is specified. The version must be of format x.x.x.x, where x must be an integer greater than or equal to 0. If omitted, version 1.0.0.0 is assumed.
=============== =================================================================================================

For each object, either ``typeid`` or ``containerid`` must be specified. If ``containerid`` is specified, the values must conform to the Type with which the Container is associated. If ``typeid`` is specified, the values must conform to that Type.

If a Type Property is defined but no property value is provided in the Data message, a default value will be assumed. Default values are specified in :doc:`Type_Properties_and_Formats`.

If ``action`` is specified, the action to be performed will apply to all entries in ``values``. 

Partial updates of data are supported by including ``action`` with a value of ``update`` and including ``patch`` with the list of properties to update in the message. When sending ``values`` any property not present in the ``patch`` array will be ignored. If a property is present in ``patch`` but not present in ``values``, the default value of the property type will be assumed as specified in :doc:`Type_Properties_and_Formats`. Index properties must always be included with values when patching data.


For example:

Assuming the type below has been defined previously:

::	

	[
	
		...
	
		{
			"id": "TankMeasurement",
			"version": "1.0.0.0",
			"type": "object",
			"classification": "dynamic",
			"properties": {
					"Time": {
						"format": "date-time",
						"type": "string",
						"isindex": true
					},
					"Pressure": {
						"type": "number",
						"name": "Tank Pressure",
						"description": "Tank Pressure in Pa",
						"uom": "pascal"
					},
					"Temperature": {
						"type": "number",
						"name": "Tank Temperature",
						"description": "Tank Temperature in K",
						"uom": "K"
					},
					"Quality": {
						"type": "integer",
						"format": "uint32",						
						"quality": "OPC UA"
					}
			}
		},
		
		...
	
	]
	
Partial updates can be sent as follows assuming a container *Tank1Measurements* with the above type registered:
	
::	

	[
		
		...
		
		{
			"containerid": "Tank1Measurements",
			"action": "update",
			"patch": ["Temperature", "Quality"],
			"values": [{
				"Time": "2017-01-11T22:23:23.430Z",
				"Temperature": 100.1,
				"Quality": 0
			}, {
				"Time": "2017-01-11T22:24:23.430Z",
				"Pressure": 11.5,
				"Quality": 1
			}]
		},
		
		...
		
	]

In this example the first entry in the ``values`` array updates *Temperature* and *Quality* only without affecting *Pressure*. The second entry also updates *Temperature* and *Quality* only without updating *Pressure*. *Pressure* is ignored, since it is not specified in ``patch``. *Temperature* will be assumed to be the default value of 0, since it is not specified in the second array entry.  
	

.. toctree::

   Data_Msg_Sample
