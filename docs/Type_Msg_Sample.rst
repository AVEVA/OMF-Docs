Type Example
^^^^^^^^^^^^^^

**Headers**

::

	producertoken = b7CNvN36cq
	version = 1.0
	messagetype = type
	messageformat = json
	action = create

**Body**

::

	[{
		"id": "Plant",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "static",
		"properties": {
			"PlantId": {
				"type": "string",
				"index": true
			},
			"PlantName": {
				"type": "string",
				"name": true
			},
			"Address": {
				"type": "string"
			},
			"Contact": {
				"type": "string"
			}
		}
	}, {
		"id": "Tank",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "static",
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
	}, {
		"id": "TankMeasurement",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "dynamic",
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
	}]

	
