Enum Types
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An ``enum`` is a Type message defined using an array of name/value pairs used to create a limited set of allowed values. 
An ``enum`` can also be used to define a a set of Data Quality values. 
When defining data quality include the ``quality`` property and specify the status `good`, `bad`, or `questionable` for each ``value`` in the enum.  


=================== =============================
Name                Value
=================== =============================
``value``			A unique numeric value associated with the enum. If not defined the enum ranges from 0 to one less than size of the collection.
``name``			A unique string that describes the condition or state being represented. This string is used as the displayed value when an enum is selected as the Type for a property.
``quality``			Optional field needed when defining an enum that holds data quality. Must be set to `good`, `bad`, or `questionable`. Defaults to 'good' when not specified.  
=================== =============================


The array definition could contain only the name property and accept the defaults for the other properties, or could contain all three properties. 

For example a Valve could have 2 states, CLOSED or OPEN and accept the defaults, or explicitly define the values:

::

	{ "id": "ValveState", "type": "object", 
	“enum”:[ "CLOSED", "OPEN"] }

	{ "id": "ValveState", "type": "object", 
	“enum”:[ {"name":"CLOSED", "value":0}, {"name":"OPEN", "value":1} ] }
	
	{ "id": "ValveState", "type": "object", 
	“enum”:[ {"value":0, "name":"CLOSED" }, {"value":1, "name":"OPEN"} ] }


An ``enum`` could be defined to represent data quality, and in this case the ``quality`` should be included in the Type message: 

::

	{ "id": "DataQualityEnum", "type": "object", 
	  "enum":[ {"name": "Device Connected", "value": 0, "quality": "good"}, 
		{"name": "Device Failure", "value": 1, "quality": "bad"},
		{"name": "Device Comm Failure", "value": 2, "quality": "bad"},
		{"name": "Uncertain - Out Limits", "value": 3, "quality": "questionable"}] }


When referencing the ``enum``, use the `isquality` identifier to denote the property that holds quality:

::

	{ "DataQuality": { "type": "object", "reftype": "DataQualityEnum", "isquality": true } }




Examples:

::
	
	[{
		"id": "ValveState",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "static",		
		"enum": [ { 
			"value": 0, 				
			"name": "CLOSED"							
		}, {
			"value": 1,
			"name": "OPEN"												
		} ]
	}, {	
		"id": "TankMeasurementv2",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "dynamic",
		"properties": {	
			"Timestamp": {                        
				"type": "string", 
				"format":"date-time",
				"isindex": true		
			},
			"ValvePosition": {			
				"type": "object",
				"reftype": "ValveState"
			}			
			"Pressure": {
				"type": "number",
				"name": "Tank Pressure",
				"description": "Tank Pressure in Pa",
				"uom": "pascal"
			},
			"Temperature": {
				"type": "number",
				"name": "Tank Temperature",
				"description": "Tank Temperature in K",
				"uom": "K" 				
			}						
		}
	}]
	
	
::
	
	[{
		"id": "DeviceQualityEnum",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "static",		
		"enum": [ { 
			"value": 0, 				
			"name": "Connected",
			"quality": "good"
		}, {
			"value": 1,
			"name":  "Updating",
			"quality": "good"											
		}, {
			"value": 2,
			"name":  "Device in error",
			"quality": "bad"											
		} , {
			"value": 3,
			"name":  "Device Down",
			"quality": "bad"											
		} , {
			"value": 4,
			"name":  "Uncertain",
			"quality": "questionable"											
		} ]
	}, {	
		"id": "TankMeasurementv3",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "dynamic",
		"properties": {			
			"Pressure": {
				"type": "number",
				"name": "Tank Pressure",
				"description": "Tank Pressure in Pa",
				"uom": "pascal"
			},
			"Temperature": {
				"type": "number",
				"name": "Tank Temperature",
				"description": "Tank Temperature in K",
				"uom": "K" 				
			},
			"Timestamp": {                        
				"type": "string", 
				"format":"date-time",
				"isindex": true		
			},
			"Quality": {
				"type": "object",
				"reftype": "DeviceQualityEnum", 
				"isquality": true
			}
		}
	}]
	