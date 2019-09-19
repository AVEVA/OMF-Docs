Type Example with Inheritance
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Properties of a Type definition can reference a previously defined Type using the ``reftype`` keyword, enabling support for inheritance and reuse of common properties.


For example, a Plant could have different types of Tanks, such as rectangular or cylindrical, where each tank shares common properties and contains additional properites:

**Headers**
::

	omfversion = 1.2
	messagetype = type
	action = create
	messageformat = json


**Body**
::

	[{
		"id": "TankMeasurements",
		"version": "1.0.0.1",
		"type": "object",
		"classification": "dynamic",
		"properties": {
			"LiquidLevel": {			
				"type": "number",
				"format":"float64",			
			},		
			"TankLength": {
				"type": "number",
				"format":"float32"
			},
			"Timestamp": {                        
				"type": "string", 
				"isindex": true,
				"format":"date-time"
			}
		}
	},{
		"id": "RectangularMeasurements",		
		"version": "1.0.0.0",
		"type": "object",
		"classification": "dynamic",
		"properties": {	
			"TankProperties": {
				"type":"object",
				"reftype":"TankMeasurements", 
				"refversion":"1.0.0.1"
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
	},{
		"id": "CylindricalMeasurements",		
		"version": "1.0.0.0",
		"type": "object",
		"classification": "dynamic",
		"properties": {
			"TankProperties": {
				"type":"object",
				"reftype":"TankMeasurements", 
				"refversion":"1.0.0.1"
			},	
			"TankDiameter": {
				"type": "number",
				"format":"float32",
				"description": "high-side reference point"					
			}
		}
	},{
		"id":"Tank",
		"version": "1.0.0.1",
		"type": "object",
		"classification": "static",
		"properties": {
			"ModelNumber": {			
				"type": "integer",
				"format":"int32",			
			},		
			"SerialNumber": {
				"type": "integer",
				"format":"int32",		
			},
			"TankName": {                        
				"type": "string", 
				"isindex": true
			}
		}
	}, {
		"id":"RectangularTank",
		"version": "1.0.0.1",
		"type": "object",
		"classification": "static",
		"properties": {
			"TankProperties": {			
				"type":"object",
				"reftype":"Tank", 
			},
			"MeasurementProperties":{
				"type":"object",
				"reftype":"RectangularMeasurements", 
			}
		}
	}, {
		"id":"CylindricalTank",
		"version": "1.0.0.1",
		"type": "object",
		"classification": "static",
		"properties": {
			"TankProperties": {			
				"type":"object",
				"reftype":"Tank", 
			},
			"MeasurementProperties":{
				"type":"object",
				"reftype":"CylindricalMeasurements", 
			}
		}
	}]
	
**Headers**
::
	
	omfversion = 1.2
	messagetype = container
	action = create
	messageformat = json

**Body**
::

	[{
		"id": "Tank1_RectangularMeasurements",
		"typeid": "RectangularMeasurements"        
	}, {
		"id": "Tank2_CylindricalMeasurements",
		"typeid": "CylindricalMeasurements"        
	}]


**Headers**
::

	omfversion = 1.2
	messagetype = data
	action = create
	messageformat = json

**Body**
::

	[{
		"typeid": "RectangularTank",
		"values": [{
			"ModelNumber":"TB-628", 
			"SerialNumber":"2554-2446-FS12",
			"TankName":"Tank1_Rectangle", 
			"MeasurementProperties": {
				"containerid": "Tank1_RectangularMeasurements"
			}
	}, {
		"typeid": "CylindricalTank",
		"values": [{
			"ModelNumber":"CK-417", 
			"SerialNumber":"6332-5159-KKF4",
			"TankName":"Tank2_Cylindrical", 
			"MeasurementProperties": {
				"containerid": "Tank2_CylindricalMeasurements"
			}
	}, {
		"containerid":"Tank1_RectangularMeasurements",
		"values":{
			"TankHeight":"123",
			"TankWidth":"200",
			"TankLength":"300",
			"LiquidLevel":"86", 
			"Timestamp":"9/18/2019 8:42:28.073 AM"
		}
	}, {
		"containerid":"Tank1_RectangularMeasurements",
		"values":{
			"TankHeight":"123",
			"TankWidth":"200",
			"TankLength":"300",
			"LiquidLevel":"86", 
			"Timestamp":"9/18/2019 8:42:28.073 AM"
		}
	}]