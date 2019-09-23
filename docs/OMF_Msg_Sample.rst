OMF v1.2 Example 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Example for creating Types, Containers and Data for ``static`` and ``dynamic`` data. 

The example shows how to setup a ``static`` Type and define the index and name properties, and shows how to setup a ``dynamic`` Type for the frequently changing data.
Next Containers are created for the ``dynamic`` Types to provide streams for data events. Lastly, data messages are used to create instances of ``static`` types, relate ``static`` and ``dynamic`` data, and send data values.


**Headers**
::

	omfversion = 1.2
	messagetype = type
	action = create
	messageformat = json


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
	}{
		"id": "TankMeasurement",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "dynamic",		
		"properties": {			
			"Pressure": {
				"type": "number",
				"name": "Tank Pressure",
				"description": "Tank Pressure in Pa",
				"uom": "pascal",
				"interpolation": "Continuous",
				"extrapolation": "Forward",
				"max": "20",
				"min": "10"
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
			},
			"Measurements": {
				"type":"object",
				"reftype":"TankMeasurement"	
			}
		}
	}]
	

Create containers for the ``dynamic`` types.


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
			"Temperature{				
				"description": "Tank Temperature in degree Fahrenheit",
				"uom": "F"
			}
		}			
	}]


Send data messages to create assets, relate instances, and send data values. 

 
**Headers**
::

	omfversion = 1.2
	messagetype = data
	action = create
	messageformat = json

**Body**
::

	[{
		"typeid": "Plant",
		"values": [{
			"PlantId": "WTP1",
			"PlantName": "Water Treatment Plant One",
			"Address": "123 Meridian Ave",
			"Contact": "Bob Ross"
		}]
	}, {
		"typeid": "Tank",
		"values": [{
			"TankName": "Tank1",
			"Serial": "5236-3523-KKF4",
			"Model": "FN-2187",
			"Measurements": {
				"containerid": "Tank1Measurements"
			}
		}, {
			"TankName": "Tank2",
			"Serial": "2364-4243-FS12",
			"Model": "TK-421",
			"Measurements": {
				"containerid": "Tank2Measurements"
			}
		}]
	}, {
		"typeid": "__Link",
		"values": [{
			"source": {
				"typeid": "Plant",
				"index": "WTP1"
			},
			"target": {
				"typeid": "Tank",
				"index": "Tank1"
			}
		}, {

			"source": {
				"typeid": "Plant",
				"index": "WTP1"
			},
			"target": {
				"typeid": "Tank",
				"index": "Tank2"
			}
		}]
	}, {
		"containerid": "Tank1Measurements",
		"values": [{
			"Time": "2019-09-11T22:23:23.430Z",
			"Pressure": 12.0,
			"Temperature": 100.1
		}, {
			"Time": "2019-09-11T22:24:23.430Z",
			"Pressure": 11.5,
			"Temperature": 101.2
		}]
	}, {
		"containerid": "Tank2Measurements",
		"values": [{
			"Time": "2019-09-11T22:23:23.430Z",
			"Pressure": 14.0,
			"Temperature": 90.1
		}, {
			"Time": "2019-09-11T22:24:23.430Z",
			"Pressure": 15.1,
			"Temperature": 91.2
		}]
	}]

	
