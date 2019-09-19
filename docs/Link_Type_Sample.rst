Link Example using Types
^^^^^^^^^^^^^^^^^^^^^^^^^

Data messages are used to create instances of Types, create relationships between instances, and send data values for static and dynamic data.

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
			"PlantId": "PlantId1",
			"PlantName": "Plant1",
			"Address": "123 Meridian Ave",
			"Contact": "Bob Ross"			
		}]
	}, {
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
		}
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