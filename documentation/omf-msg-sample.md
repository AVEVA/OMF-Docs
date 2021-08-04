---
uid: OMFMsgSample
---

# OMF Example 

Example for creating Types, Containers and Data for `static` and `dynamic` data. 

The example shows how to setup a `static` Type and define the index and name properties, and shows how to setup a `dynamic` Type for the frequently changing data.
Next Containers are created for the `dynamic` Types to provide streams for data events. Lastly, data messages are used to create instances of `static` types, relate `static` and `dynamic` data, and send data values.


### Type Message Headers

	omfversion = 1.2
	messagetype = type
	action = create
	messageformat = json

### Type Message Body

	[{
		"id": "Plant",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "static",
		"extrapolation": "all",
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
	},{
		"id": "TankMeasurement",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "dynamic",	
		"extrapolation": "forward",
		"properties": {			
			"Pressure": {
				"type": "number",
				"name": "Tank Pressure",
				"description": "Tank Pressure in Pa",
				"uom": "pascal",
				"interpolation": "continuous",
				"max": "20",
				"min": "10"
			},
			"Temperature": {
				"type": "number",
				"name": "Tank Temperature",
				"description": "Tank Temperature in K",
				"uom",
				"interpolation": "continuous"
			},
			"Timestamp": {                        
				"type": "string", 
				"format":"date-time",
				"isindex": true,
				"interpolation": "continuous"
			}
		}
	},{ 	
		"id":"LocationProperties",
		"type":"object",
		"properties": { 
			"Latitude":{ "type":"number", "format":"float32" },
			"Longitude":{ "type":"number", "format":"float32" }
		}
	},{
		"id": "TankV2",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "static",
	        "extrapolation": "all",
		"properties": {
			"TankName": {
				"type": "string",				
				"isname": true,
				"isindex":true
			},
			"Serial": {
				"type": "string"
			},
			"Model": {
				"type": "string"
			},
			"Location": {
				"reftypeid": "LocationProperties"
			}
		}
	}, {
		"id":"RectangularTank",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "static",
	        "extrapolation": "all",
		"basetypeid": "TankV2",
		"properties": {					
			"TankHeight": {
				"type": "integer",
				"format":"int32",
				"uom":"ft"				
			},
			"TankWidth": {
				"type": "integer",
				"format":"int32",
				"uom":"ft"
			}	
		}
	}]

Create containers for the `dynamic` types.

### Container Message Headers

    omfversion = 1.2
    messagetype = container
    action = create
    messageformat = json

### Container Message Body

	[{
		"id": "Tank1Measurements",
		"typeid": "TankMeasurement",
		"indexes": ["Pressure"], 
		"datasource":"Modbus",
		"extrapolation": "forward"
	}, {
		"id": "Tank2Measurements",
		"typeid": "TankMeasurement",
		"datasource":"Modbus",	
		"propertyoverrides": {
			"Temperature": {				
				"description": "Tank Temperature in degree Fahrenheit",
				"uom": "F"
			}
		}			
	}, {
		"id": "Tank_R1_Measurements",
		"typeid": "TankMeasurement",
		"datasource":"Modbus"
	}]


Send data messages to create assets, relate instances, and send data values, for static, dynamic and type-less data instances. 

### Data Message Headers

    omfversion = 1.2
    messagetype = data
    action = create
    messageformat = json

### Data Message Body

	[{
		"typeid": "Plant",
		"values": [{
			"PlantId": "WTP1",
			"PlantName": "Water Treatment Plant One",
			"Address": "123 Meridian Ave",
			"Contact": "Bob Ross"
		}]
	}, {
		"typeid": "TankV2",
		"values": [{
			"TankName": "Tank1",
			"Serial": "5236-3523-KKF4",
			"Model": "FN-2187",
			"Location": {
				"Latitude": 36.3134,
				"Longitude": -82.3535 
			}	
		}, {
			"TankName": "Tank2",
			"Serial": "2364-4243-FS12",
			"Model": "TK-421"	,
			"Location": {
				"Latitude": 45.4046,
				"Longitude": -122.579 
			}			
		}]
	}, {
		"typeid": "RectangularTank",
		"values": [{
			"TankName": "Tank_R1",
			"Serial": "4738-9283-CKD4",
			"Model": "SD-3947",
			"Location": {
				"Latitude": 52.273,
				"Longitude": -95.2834 
			},
			"TankHeight": 100,
			"TankWidth": 80
		}]
	}, { 	   
       "properties": { 
			"Name": {
				"type":"string",
				"isindex":true
			},
			"Description": {
				"type":"string"
			},
			"Model": {
				"type":"string"
			},			
            "HourlyMaintenanceSchedule": {
				"type": "integer",
                "format": "int16"
			}
        }, 
        "values": [{ 
              "Name": "Tank4", 
              "Description": "Tank4 in Building C12", 
              "Model": "EK-2393",
			  "HourlyMaintenanceSchedule": 8
        }] 
	}, {
		"typeid": "__Link",
		"values": [{
			"source": {
				"typeid": "Plant",
				"index": "WTP1"
			},
			"target": {
				"typeid": "TankV2",
				"index": "Tank1"
			}
		}, {
			"source": {
				"typeid": "Plant",
				"index": "WTP1"
			},
			"target": {
				"typeid": "TankV2",
				"index": "Tank2"
			}
		}, {
			"source": {
				"typeid": "Plant",
				"index": "WTP1"
			},
			"target": {
				"typeid": "RectangularTank",
				"index": "Tank_R1"
			}
		}, {
			"source": {
				"typeid": "TankV2",
				"index": "Tank1"
			},
			"target": {
				"containerid": "Tank1Measurements"
			}
		}, {
			"source": {
				"typeid": "TankV2",
				"index": "Tank2"
			},
			"target": {
				"containerid": "Tank2Measurements"
			}
		}, {
			"source": {
				"typeid": "RectangularTank",
				"index": "Tank_R1"
			},
			"target": {
				"containerid": "Tank_R1_Measurements"
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
	}, {
		"containerid": "Tank_R1_Measurements",
		"values": [{
			"Time": "2019-09-11T22:23:23.430Z",
			"Pressure": 13.0,
			"Temperature": 93.5
		}, {
			"Time": "2019-09-11T22:24:23.430Z",
			"Pressure": 12.6,
			"Temperature": 97.1
		}]
	}]
