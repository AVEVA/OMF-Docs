---
uid: typeExample
---

# Type Example


### Headers

    producertoken = b7CNvN36cq
	omfversion = 1.0
    messagetype = type
    action = create
    messageformat = json


### Body

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
            "TankName": {
                "type": "string",
                "isindex": true,
                "isname": true              
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


### Array Property Example

In this example we define a property of type `array`. The type of items contained by the array is specified via the
`items` keyword.

	[{
		"id": "MaintenanceSchedule",
		"type": "object",
		"classification": "static",
		"properties": {
			"Name": { "type": "string", "isindex": true, "isname": true },
			"Maintenance Schedule": {
				"type": "array",
				"items": {
					"type": "string",
					"format": "date-time"
				}
			},
			"Maintenance Performed By": {
				"type": "string"
			}
		}
	]