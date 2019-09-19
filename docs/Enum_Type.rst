Type Example with Enumerations 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An ``enum`` is an array of name/value pairs in a Type defintion, used to create a limited set of allowed values. An ``enum`` can also be used to define a a set of Data Quality values and their ``status``. 


=================== =============================
Name                Value
=================== =============================
``value``			A unique numeric value associated with the enumeration. Provides a quicker, less memory-intensive representation of the data. If not defined the enumeration set ranges from 0 to one less than size of the collection.
``name``			A unique string that describes the condition or state being represented. This string is used as the displayed value when an enumeration set is selected as the Type for a property.
``status``			Optional field used when defining an enumeration set that defines Data Quality. Must be set to `good`, `bad`, or `questionable`. Defaults to 'good' when not specified.  
=================== =============================


The array definition could contain only the name property and accept the defaults for the other properties, or could contain all three properties. 

For example a Valve could have 2 states, CLOSED or OPEN and accept the defaults:

::

	{ "id": "ValveState", "type": "object", “enum”:[ "CLOSED", "OPEN"] }




An enumeration set could be defined to represent data quality, and in this case the ``status`` should be set: 

::

	{ "id": "DataQualityEnum", 
	  "type": "object", 
	  "enum":[ {"name": "Device Connected", "value": 0, "status": "good"}, 
		{"name": "Device Failure", "value": 1, "status": "bad"},
		{"name": "Device Comm Failure", "value": 2, "status": "bad"},
		{"name": "Uncertain - Out Limits", "value": 3, "status": "questionable"}] }


When referencing the enumeration set, use the `isquality` identifer to denote the property that holds quality:

::

	{ "DataQuality": { "type": "object", "reftype": "DataQualityEnum", "isquality": true } }




Enumeration Example:

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
		"id": "Tank",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "dynamic",
		"properties": {
			"Valve": {			
				"type": "object",
				"reftype": "ValveState"
			}
			"LiquidLevel": {			
				"type": "number",
				"format": "float64",			
			},		
			"TankLength": {
				"type": "number",
				"format": "float32"
			}
		}
	}]
	