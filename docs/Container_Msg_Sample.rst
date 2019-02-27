Container Example
^^^^^^^^^^^^^^^^^^

**Headers**

::

	producertoken = b7CNvN36cq
	omfversion = 1.2
	messagetype = container
	action = create
	messageformat = json


**Body**

::

	[{
		"id": "Tank1Measurements",
		"typeid": "TankMeasurement",
		"typeVersion": "1.0.0.0",
		"dataSource": "tankDS",
		"indexes": ["Pressure"]
	}, {
		"id": "Tank2Measurements",
		"typeid": "TankMeasurement",
		"typeVersion": "1.0.0.0",
		"propertyoverrides": {
			"Pressure": {
				"name": "Particular Tank Pressure",
				"description": "Tank Pressure in atm",
				"uom": "atm"
			}
		}
	}]
