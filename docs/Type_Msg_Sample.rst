Type Example 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the following example we create 2 ``static`` types and a ``dynamic`` type. The Type definitions define properties for the ``isindex`` and ``isname`` qualifiers. Their values will referenced later when defining instance data and creating relationships.


**Headers**
::

	omfversion = 1.2
	messagetype = type
	action = create
	messageformat = json


**Body**
::

	[{
		"id": "Plant",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "static",
		"properties": {
			"PlantId": {
				"type": "string",
				"isindex": true
			},
			"PlantName": {
				"type": "string",
				"isname": true
			},
			"Address": {
				"type": "string"
			},
			"Contact": {
				"type": "string"
			}
		}
	}, {
		"id": "Tank",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "static",		
		"properties": {
			"TankName": {
				"type": "string",
				"isindex": true,
				"isname": true				
			},
			"Serial": {
				"type": "string"
			},
			"Model": {
				"type": "string"
			}
		}
	}, {
		"id": "TankMeasurement",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "dynamic",		
		"properties": {	
			"Timestamp": {                        
				"type": "string", 
				"format":"date-time",
				"isindex": true		
			}		
			"Pressure": {
				"type": "number",
				"name": "Tank Pressure",
				"description": "Tank Pressure in Pa",
				"uom": "pascal",
				"interpolation": "Continuous",
				"extrapolation": "Forward",
				"max": "20",
				"min": "10"
			},
			"Temperature": {
				"type": "number",
				"name": "Tank Temperature",
				"description": "Tank Temperature in K",
				"uom": "K" 				
			}			
		}
	}]



Properties of a Type definition can reference a previously defined Type using the ``reftype`` keyword, enabling support for ``static`` and ``dynamic`` data in a single Type definiton. 
In this example we reference the previously defined TankMeasurement Type within the new Tankv2 ``static`` type:

::

	[{
		"id": "Tankv2",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "static",		
		"properties": {	
			"TankName": {
				"type": "string",
				"isindex": true
			},
			"Measurements": {
				"type":"object",
				"reftype":"TankMeasurement"	
			},		
			"Maintenance Schedule": {
				"type": "array",
				"items": { 
					"type": "string",
					"format": "date-time"
				}
			},
			"Location": {
				"type": "object",
				"properties": {
					"Latitude": {
						"type": "number"
					},
					"Longitude": {
						"type": "number"
					}
				}
			}				
		}
	}]
	

Using the ``reftype`` keyword, a Type can be created from multiple previously defined Types. For example:  

::

	[{
		"id":"RectangularTank",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "static",
		"properties": {
			"TankProperties": {			
				"type":"object",
				"reftype":"Tank" 
			},
			"Measurements": {
				"type":"object",
				"reftype":"TankMeasurement"	
			},	
			"TankHeight": {
				"type": "number",
				"format":"float64",			
			},
			"TankWidth": {
				"type": "number",
				"format":"float32",				
				"description": "Temperature in K",
				"uom": "K"
			}	
		}
	}, {
		"id":"CylindricalTank",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "static",
		"properties": {
			"TankProperties": {			
				"type":"object",
				"reftype":"Tank" 
			},
			"Measurements": {
				"type":"object",
				"reftype":"TankMeasurement"	
			},			
			"TankDiameter": {
				"type": "number",
				"format":"float32",
				"description": "high-side reference point"					
			}
		}
	}]
