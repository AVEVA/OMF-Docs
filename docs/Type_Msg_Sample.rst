Sample
^^^^^^

**Headers**

::

	producertoken = b7CNvN36cq
	version = 0.9.0.0
	messagetype = types
	action = create

**Body**

::

	[
	{
		"id": "TankMeasurement",
		"version": "1.0.0.0",
		"type": "object",
		"properties": {
			"Time": {
				"format": "date-time",
				"type": "string",
				"index": true
			},
			"Pressure": {
				"type": "number"
			},
			"Temperature": {
				"type": "number"
			}
		}
	},
	{
		"id": "Tank",
		"version": "1.0.0.0",
		"type": "object",
		"properties": {
			"Name": {
				"type": "string",
				"index": true
			},
			"Serial": {
				"type": "string"
			},
			"Model": {
				"type": "string"
			}
		}
	}
	]
	
