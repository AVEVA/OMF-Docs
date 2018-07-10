Data Messages
-------------

Data messages can span multiple Types and Containers. Data can be created, updated, deleted, or patched.

The body of a Data message is composed of an array of objects with the following keywords: 

=============== =================================================================================================
Name            Value
=============== =================================================================================================
``values`` 	    An array of objects conforming to the type.
``action``      Optional: One of: ``create``, ``update``, ``delete``, or ``patch``. The value specified overrides the value of the ``action`` header. If omitted, the value of the ``action`` header is assumed. See :doc:`Headers`.
``containerid`` Optional ID of the container. If omitted, type is expected.
``typeid``      Optional ID of the type. If omitted, container is expected.
``typeversion`` Optional version of the Type, if one is specified. If omitted, version 1.0.0.0 is assumed.
=============== =================================================================================================

For each object, either ``typeid`` or ``containerid`` must be specified. If ``containerid`` is specified, the values must conform to the Type with which the Container is associated. If ``typeid`` is specified, the values must conform to that Type.

If a Type Property is defined but no property value is provided in the Data message, a default value will be assumed. Default values are specified in :doc:`Type_Properties_and_Formats`.

If ``action`` is specified, the action to be performed will apply to all entries in ``values``. 

Partial updates of data are supported by including ``action`` with a value of ``patch`` in the message. For example:

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
                        "isquality": true,
                        "qualityscheme": "OPC UA"
					}
			}
		},
		
		...
	
	]
	
Partial updates can be sent as follows:
	
::	

	[
		
		...
		
		{
			"containerid": "Tank1Measurements",
			"action": "patch",
			"values": [{
					"Time": "2017-01-11T22:23:23.430Z",					
					"Temperature": 100.1
					"Quality": 0
			}, {
					"Time": "2017-01-11T22:24:23.430Z",
					"Pressure": 11.5					
					"Quality": 1
			}]
		},			
		
		...
		
	]

In this example the first entry in the ``values`` array updates *Temperature* only without affecting *Pressure* while the second entry updates *Pressure* only without updating *Temperature*.
	

.. toctree::

   Data_Msg_Sample
