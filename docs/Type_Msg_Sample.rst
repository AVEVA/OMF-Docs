Sample
^^^^^^

**Headers**

::

	producertoken = b7CNvN36cq
	version = 1.0
	messagetype = type
	messageformat = json
	action = create

**Body**

::

	[{
		"id": "TankMeasurement",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "value",
		"properties": {
			"Time": {
				"format": "date-time",
				"type": "string",
				"index": true
			},
			"Pressure": {
				"type": "number"
			},
			"Temperature": {
				"type": "number"
			}
		}
	}, {
		"id": "Tank",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "value",
		"properties": {
			"Name": {
				"type": "string",
				"index": true
			},
			"Serial": {
				"type": "string"
			},
			"Model": {
				"type": "string"
			}
		}
	}, {
		"id": "OverRange",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "span",
		"properties": {
			"ID": {
				"type": "string",
				"index": true
			},
			"StartTime": {
				"format": "date-time",
				"type": "string"
			},
			"EndTime": {
				"format": "date-time",
				"type": "string"
			}
		}
	}, {
		"id": "TankLink",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "link",
		"properties": {
			"ID": {
				"type": "string",
				"index": true
			},
			"source": {
				"type": "string",
				"linktype": "Tank"
			},
			"target0": {
				"type": "string",
				"linktype": "Tank"
			},
			"target1": {
				"type": "string",
				"linktype": "Pump",
				"linktypeversion": "2.0.0.0"
			}

		}
	}]

	
