Value Type Sample
^^^^^^^^^^^^^^^^^

::

	{
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
	}
		
