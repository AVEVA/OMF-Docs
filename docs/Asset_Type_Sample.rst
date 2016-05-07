Asset Type Sample
^^^^^^^^^^^^^^^^^

::

	{
		"id": "OverRange",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "span"
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
	}
