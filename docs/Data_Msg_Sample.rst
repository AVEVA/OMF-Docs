Sample
^^^^^^

**Headers**

::

	producertoken = b7CNvN36cq
	version = 0.9.0.0
	messagetype = values
	action = create
	messageformat = json

**Body**

::

	[
	{
	    "streamId": "Building1TankMeasurements",
	    "values": [
	    { "Time": "2015-12-31T22:33:39.069083Z", "Pressure": 25.4, "Temperature": 120.542 },
	    { "Time": "2015-12-31T22:33:39.069083Z", "Pressure": 25.4, "Temperature": 120.542 },
	    { "Time": "2015-12-31T22:33:39.069083Z", "Pressure": 25.4, "Temperature": 120.542 },
	    { "Time": "2015-12-31T22:33:39.069083Z", "Pressure": 25.4, "Temperature": 120.542 }
	    ]
	},
	{
	    "streamId": "Tanks",
	    "values": [
	    { "Name": "Building1", "Serial": "5236-3523-KKF4", "Model": "FN-2187" },
	    { "Name": "Building2", "Serial": "2364-4243-FS12", "Model": "TK-421" }
	    ]
	}
	]

