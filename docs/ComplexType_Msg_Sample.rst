Type Example 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Properties of a Type definition can reference a previously defined Type using the ``reftype`` keyword, enabling support for static and dynamic data in a single Type definiton.

	
In this example we define a dynamic type and a static type that includes the dynamic type:

**Headers**
::

	omfversion = 1.2
	messagetype = type
	action = create
	messageformat = json


**Body**
::

	[{
		"id": "TankMeasurement",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "dynamic",		
		"properties": {			
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
			"Timestamp": {                        
				"type": "string", 
				"format":"date-time",
				"isindex": true		
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
				"isindex": true,
				"isname": true				
			},
			"Serial": {
				"type": "string"
			},
			"Model": {
				"type": "string"
			},
			"Measurements": {
				"type":"object",
				"reftype":"TankMeasurement"	
			}
		}
	}, {
		"id": "Tankv2",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "static",		
		"properties": {					
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
			},
			"Measurements": {
				"type":"object",
				"reftype":"TankMeasurement"	
			}	
		}
	}, {
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
	}]
	
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
		"typeVersion": "1.0.0.0"
	}, {
		"id": "Tank2Measurements",
		"typeid": "TankMeasurement",
		"typeVersion": "1.0.0.0"
	}]



**Headers**
::

	omfversion = 1.2
	messagetype = data
	action = create
	messageformat = json

**Body**
::

	[{
		"typeid": "Tank",
		"values": [{
			"Name": "Tank1",
			"Serial": "5236-3523-KKF4",
			"Model": "FN-2187",
			"Measurements": {
				"containerid": "Tank1Measurements"
			}
		}, {
			"Name": "Tank2",
			"Serial": "2364-4243-FS12",
			"Model": "TK-421",
			"Measurements": {
				"containerid": "Tank2Measurements"
			}
		}]
	}, {		
		"containerid": "Tank1Measurements",
		"values": [{			
			"Pressure": 12.0,
			"Temperature": 100.1,
			"Timestamp": "2019-08-11T22:23:23.430Z",
		}, {			
			"Pressure": 11.5,
			"Temperature": 101.2,
			"Timestamp": "2019-08-11T22:24:23.430Z",
		}]
	}, {
		"containerid": "Tank2Measurements",
		"values": [{			
			"Pressure": 14.0,
			"Temperature": 90.1,
			"Timestamp": "2019-08-11T22:23:23.430Z",
		}, {			
			"Pressure": 15.1,
			"Temperature": 91.2,
			"Timestamp": "2019-08-11T22:24:23.430Z",
		}]
	}]]


	