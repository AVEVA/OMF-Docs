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
				"uom": "K",
				"interpolation": "continuous"
			},
			"Timestamp": {
				"type": "string",
				"format": "date-time",
				"isindex": true
			}
		}
	},{
		"id": "LocationProperties",
		"type": "object",
		"properties": {
			"Latitude":{ "type": "number", "format": "float32" },
			"Longitude":{ "type": "number", "format": "float32" }
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
		"datasource": "Modbus",
		"extrapolation": "forward"
	}, {
		"id": "Tank2Measurements",
		"typeid": "TankMeasurement",
		"datasource": "Modbus",
		"propertyoverrides": {
			"Temperature": {
				"description": "Tank Temperature in degree Fahrenheit",
				"uom": "F"
			}
		}
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
			"Model": "TK-421",
			"Location": {
				"Latitude": 45.4046,
				"Longitude": -122.579
			}
		}]
	}, {
       "properties": {
			"Name": {
				"type": "string",
				"isindex":true
			},
			"Description": {
				"type": "string"
			},
			"Model": {
				"type": "string"
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
