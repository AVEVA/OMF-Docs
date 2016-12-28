Sample
^^^^^^

**Headers**

::

	producertoken = b7CNvN36cq
	version = 0.12
	messagetype = type
	action = create

**Body**

::

	[
	{
		"id": "TankMeasurement",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "stream",
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
	},
	{
		"id": "Tank",
		"version": "1.0.0.0",
		"type": "object",
	        "classification": "asset",
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
	},
	{
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
	},
	{
	        "id": "TankLink",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "link",
		"properties": {
		        "ID": {
			        "type": "string",
				"index": true
			},
			"Source": {
			        "type": "string",
				"linkType": "Tank"
			},
			"Target0": {
			        "type": "string",
				"linkType": "Tank"
			},
			"Target1": {
			        "type": "string",
				"linkType": "Pump",
				"linkTypeVersion": "2.0.0.0"
			}
		}
	}	
	]
	
