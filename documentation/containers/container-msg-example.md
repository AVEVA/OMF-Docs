---
uid: containerExample
---

# Container Example

### Headers

    omfversion = 1.2
	messagetype = container
	action = create
	messageformat = json

### Body

    [{
		"id": "Tank1_PressureMeasurements",
		"typeid": "TankPressure",
		"datasource":"Modbus",
		"indexes": ["Pressure"],
		"extrapolation": "forward"
	}, {
		"id": "Tank2_PressureMeasurements",
		"typeid": "TankPressure",
		"datasource":"Modbus",
		"indexes": ["Pressure"],
		"extrapolation": "forward",
		"propertyoverrides": {
			"Pressure": {
				"minimum": 15,
				"maximum": 30
			}
		}
	}]

## Delete Example

If the `action` header value is `delete` then only `id` and `typeid` are required. All other keywords are ignored.

    [{
		"id": "Tank1_PressureMeasurements",
		"typeid": "TankPressure"
	}, {
		"id": "Tank2_PressureMeasurements",
		"typeid": "TankPressure"
	}]