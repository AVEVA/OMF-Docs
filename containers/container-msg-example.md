---
uid: containerExamplev10
---

# Container Example

### Headers

    producertoken = b7CNvN36cq
	omfversion = 1.0
	messagetype = container
	action = create
	messageformat = json


### Body

    [{
		"id": "Tank1Measurements",
		"typeid": "TankMeasurement",
		"typeVersion": "1.0.0.0"		
	}, {
		"id": "Tank2Measurements",
		"typeid": "TankMeasurement",
		"typeVersion": "1.0.0.0"	
	}]
