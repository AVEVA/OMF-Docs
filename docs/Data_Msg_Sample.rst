Sample
^^^^^^

**Headers**

::

	producertoken = b7CNvN36cq
	omfversion = 1.0
	messagetype = data
	action = create
	messageformat = json

**Body**

::

	[{
		"type": "Tank",
		"values": [{
			"Name": "Building1",
			"Serial": "5236-3523-KKF4",
			"Model": "FN-2187"
		}, {
			"Name": "Building2",
			"Serial": "2364-4243-FS12",
			"Model": "TK-421"
		}]
	}, {
		"group": " Building1TankMeasurements",
		"values": [{
			"Time": "2017-01-11T22:23:23.430Z",
			"Pressure": "12.0",
			"Temperature": "100.1"
		}, {
			"Time": "2017-01-11T22:24:23.430Z",
			"Pressure": "11.5",
			"Temperature": "101.2"
		}]
	}, {
		"type": "TankLink",
		"values": [{
			"source": "Building1",
			"target0": "Building2",
			"target1": "Pump1"
		}]
	}, {
		"type": "OverRange",
		"values": [{
			"starttime": "2017-01-12T00:00:00.000Z",
			"endtime": "2017-01-11T00:00:00.000Z"
		}]
	}]





