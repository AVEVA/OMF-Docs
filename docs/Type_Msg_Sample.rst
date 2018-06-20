Type Example
^^^^^^^^^^^^^^

**Headers**

::

	producertoken = b7CNvN36cq
	omfversion = 1.2-alpha1
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
	}, {
		"id": "Tank2",
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
	}, {
		"id": "Tank2",
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

	


	
