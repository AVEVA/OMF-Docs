---
uid: enumType
---

# Enum Type Messages

An `enum` is a Type message defined using an array of name/value pairs used to create a limited set of allowed values. Once defined, the `enum` can be referenced by Properties within other Type messages.

An `enum` can also be used to define a a set of Data Quality values. 
When defining data quality include the `quality` property in the enum definition, and denote the quality as `good`, `bad`, or `questionable`.  

To define an `enum` Type, include the following keywords. If a keyword is not specified, then the default value will be used.

| Name | Value |
| --- | --- |
| `name` | A unique string that describes the condition or state being represented. This string is used as the displayed value when an enum is selected as the Type for a property. |
| `value` | Optional integer value associated with the enum. If not defined the enum ranges from 0 to one less than size of the collection. The integer value is typically used when sending data of this type. |
| `quality` | Optional field needed when defining a set of data quality values. Must be set to `good`, `bad`, or `questionable`. Defaults to \'good\' when not specified. |

The `enum` definition could contain only the name property and accept the defaults for the other properties, or explicitly define all the properties. 

For example a Valve could have 2 states, CLOSED or OPEN and accept the defaults, or explicitly define the values. The following Type messages are valid syntax:

	{ 
		"id": "ValveState", 
		"enum":[ "CLOSED", "OPEN"] 
	}

	{ 
		"id": "ValveState", 
		"enum": [ {"name":"CLOSED", "value":0}, {"name":"OPEN", "value":1} ] 
	}
	
	{ 
		"id": "ValveState", 
		"enum":[ {"value":0, "name":"CLOSED" }, {"value":1, "name":"OPEN"} ] 
	}


# Enum Type Messages for Data Quality

The following Type message defines a data quality `enum`.

An `enum` could be used to define a set of allowed values that represents data quality. In this case include the `quality` in the `enum` definition. 
If quality is not explicitly set then it is assumed to be \'good\'.

	{ 
		"id": "DeviceStatusEnum", 
		"enum":[ 
			{ "name": "Device Connected", "value": 0 },
			{ "name": "Device Failure", "value": 1, "quality": "bad" },
			{ "name": "Device Comm Failure", "value": 2, "quality": "bad" },
			{ "name": "Uncertain - Out Limits", "value": 3, "quality": "questionable" } 
		] 
	}


When referencing the `enum` from the property that holds quality, include the [isquality](xref:typePropertiesAndFormats) keyword and use `reftypeid` as the data type of the property:

    { "DeviceStatus": { "reftypeid": "DeviceStatusEnum", "isquality": true } }



### Examples


	[{
        "id": "ValveState",
        "version": "1.0.0.0",        
        "enum": [ {"name":"CLOSED", "value":0}, {"name":"OPEN", "value":1} ] 
	}, { 
        "id": "DeviceStatusEnum", 
		"enum":[ 
			{ "name": "Device Connected", "value": 0, "quality": "good" },
			{ "name": "Device Failure", "value": 1, "quality": "bad" },
			{ "name": "Device Comm Failure", "value": 2, "quality": "bad" },
			{ "name": "Uncertain - Out Limits", "value": 3, "quality": "questionable" } 
		] 
    }, {
        "id": "TankMeasurementV1",
        "version": "1.0.0.0",
        "type": "object",
        "classification": "dynamic",
        "properties": {
                "Timestamp": {
                        "type": "string",
                        "format":"date-time",
                        "isindex": true
                },
				"DeviceStatus": {
					"reftypeid": "DeviceStatusEnum", 
					"isquality": true
				},
                "ValvePosition": {
                        "reftypeid": "ValveState"
                },
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
