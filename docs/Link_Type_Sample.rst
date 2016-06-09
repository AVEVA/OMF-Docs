Link Type Sample
^^^^^^^^^^^^^^^^

::

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
                        	"LinkSchema": "Tank"
			},
			"Target0": {
				"type": "string",
                        	"LinkSchema": "Tank"
			},
			"Target1": {
				"type": "string",
                        	"LinkSchema": "Tank"
			}
		}
	}
