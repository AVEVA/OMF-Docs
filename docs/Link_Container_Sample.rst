Link Example using Type and Container
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Data messages are used to create instances of Types, create relationships between instances, and send data values for static and dynamic data.

When creating instances of Types, the Type defintion can include the reference to another Type, or the data can be linked when creating instances to form relationships.

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
			"Model": "TK-421"
		}]
	}, {
		"typeid": "__Link",
		"values": [{
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