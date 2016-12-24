Sample
^^^^^^

**Headers**

::

	producertoken = b7CNvN36cq
	version = 0.11.0.0
	messagetype = data
	action = create
	messageformat = json

**Body**

::

	[
	{
	    "stream": "Building1TankMeasurements",
	    "values": [
	    { "Time": "2015-12-31T22:33:39.069083Z", "Pressure": 25.4, "Temperature": 120.542 },
	    { "Time": "2015-12-31T22:34:39.069083Z", "Pressure": 25.6, "Temperature": 120.784 },
	    { "Time": "2015-12-31T22:35:39.069083Z", "Pressure": 25.7, "Temperature": 122.242 },
	    { "Time": "2015-12-31T22:36:39.069083Z", "Pressure": 25.9, "Temperature": 123.423 }
	    ]
	},
	{
	    "stream": "Building2TankMeasurements",
	    "values": [
	    { "Time": "2015-12-31T22:33:39.069083Z", "Pressure": 29.4, "Temperature": 129.542 },
	    { "Time": "2015-12-31T22:34:39.069083Z", "Pressure": 30.1, "Temperature": 130.223 },
	    { "Time": "2015-12-31T22:35:39.069083Z", "Pressure": 30.8, "Temperature": 130.852 }
	    ]
	}
	]

