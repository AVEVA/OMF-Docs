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
                        	"linkTypeId": "Tank"
			},
			"Target0": {
				"type": "string",
                        	"linkTypeId": "Tank"
			},
			"Target1": {
				"type": "string",
                        	"linkTypeId": "Tank",
			}
		}
	}
