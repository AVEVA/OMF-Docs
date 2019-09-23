Data Example
^^^^^^^^^^^^^

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