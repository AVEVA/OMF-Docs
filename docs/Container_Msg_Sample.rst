Container Example
^^^^^^^^^^^^^^^^^^

**Headers**

::
	
	omfversion = 1.2
	messagetype = container
	action = create
	messageformat = json


**Body**

::

	[{
		"id": "Tank1Measurements",
		"typeid": "TankMeasurement",
		"indexes": ["Pressure"], 
		"metadata": {
			"datasource":"Modbus"
		},
	}, {
		"id": "Tank2Measurements",
		"typeid": "TankMeasurement",
		"metadata": {
			"datasource":"Modbus"
		}		
		"propertyoverrides": {
			"Temperature": {				
				"description": "Tank Temperature in degree Fahrenheit",
				"uom": "F"
			}
		}			
	}]

