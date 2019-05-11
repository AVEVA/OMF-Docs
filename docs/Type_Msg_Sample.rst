Type Example
^^^^^^^^^^^^^^

**Headers**

::

	producertoken = b7CNvN36cq
	omfversion = 1.0
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
				"isindex": true
			},
			"PlantName": {
				"type": "string",
				"isname": true
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
				"isindex": true
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
				"isindex": true
			},
			"Pressure": {
				"type": "number",
				"name": "Tank Pressure",
				"description": "Tank Pressure in Pa"
			},
			"Temperature": {
				"type": "number",
				"name": "Tank Temperature",
				"description": "Tank Temperature in K"
			}
		}
	}, {
		"id": "ComplexTank",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "static",
		"properties": {
			"Name": {
				"type": "string",
				"isindex": true
			},
			"Dimensions": {
				"type": "object",
				"format": "dictionary",
				"additionalProperties": {
					"type": "number",
					"format": "float64"
				}
			},
			"Maintenance Schedule": {
				"type": "array",
				"items": { 
					"type": "string",
					"format": "date-time"
				}
			},
			"Location": {
				"type": "object",
				"properties": {
					"Latitude": {
						"type": "number"
					},
					"Longitude": {
						"type": "number"
					}
				}
			}
		}
	}]

	


	
