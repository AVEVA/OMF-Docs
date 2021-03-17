---
uid: dataExample
---

# Data Example


### Headers

	producertoken = b7CNvN36cq
	omfversion = 1.0
	messagetype = data
	action = create
	messageformat = json

### Body


	[{
        "typeid": "Plant",
        "values": [{
                "PlantId": "PlantId1",
                "PlantName": "Plant1",
                "Address": "123 Meridian Ave",
                "Contact": "Bob Ross"
        }]
	}, {
        "typeid": "Tank",
        "values": [{
                "TankName": "Tank1",
                "Serial": "5236-3523-KKF4",
                "Model": "FN-2187"
        }, {
                "TankName": "Tank2",
                "Serial": "2364-4243-FS12",
                "Model": "TK-421"
        }]
	}, {
		"typeid": "__Link",
        "values": [{
                "source": {
                        "typeid": "Plant",
                        "index": "PlantId1"
                },
                "target": {
                        "typeid": "Tank",
                        "index": "Tank1"
                }
        }, {

                "source": {
                        "typeid": "Plant",
                        "index": "PlantId1"
                },
                "target": {
                        "typeid": "Tank",
                        "index": "Tank2"
                }
        }, {

                "source": {
                        "typeid": "Tank",
                        "index": "Tank1"
                },
                "target": {
                        "containerid": "Tank1Measurements"
                }
        }, {

                "source": {
                        "typeid": "Tank",
                        "index": "Tank2"
                },
                "target": {
                        "containerid": "Tank2Measurements"
                }
        }]
	}, {
		"containerid": "Tank1Measurements",
        "values": [{
                "Time": "2017-01-11T22:23:23.430Z",
                "Pressure": 12.0,
                "Temperature": 100.1
        }, {
                "Time": "2017-01-11T22:24:23.430Z",
                "Pressure": 11.5,
                "Temperature": 101.2
        }]
	}, {
        "containerid": "Tank2Measurements",
        "values": [{
                "Time": "2017-01-11T22:23:23.430Z",
                "Pressure": 14.0,
                "Temperature": 90.1
        }, {
                "Time": "2017-01-11T22:24:23.430Z",
                "Pressure": 15.1,
                "Temperature": 91.2
        }]
	}]
