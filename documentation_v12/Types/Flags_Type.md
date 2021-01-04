---
uid: flagsEnumType
---

# Flags enum Type Messages

A `flag` enum is a Type message defined using an array of name/value pairs used to create a limited set of allowed values where multiple can be set at the same time. Once defined, the `flags` enum can be referenced by Properties within other Type messages.

## Flags enum Type Properties

The following keywords are used to define Flags enum Type definition.

| Name | Value |
| --- | --- |
| `type` | Optional type of the Flags definition. The only currently supported type is integer. Default: integer |
| `format` | Optional format of the type property. Defines how many flags can be defined. Must be from the OMF 1.2 'supported' formats table. Default: int32 |
| `values` | Array of name/value pairs used to create a limited set of allowed values. When enum is used to define a set of Data Quality values quality property can be included to denote the quality as good, bad, or questionable. |

## Flags values collection keywords
To define values possible values of an `flags` enum type, include the following keywords. If a keyword is not specified the default is going to be used.

| Name | Value |
| --- | --- |
| `name` | A unique string that describes the condition or state being represented. This string is used as the displayed value when an enum is selected as the Type for a property. |
| `value` | Required integer value associated with the enum. If not defined the enum ranges from 1 to one less than bit size of the specified `format`. The integer value is typically used when sending data of this type. |
| `quality` | Optional field needed when defining a set of data quality values. Must be set to `good`, `bad`, or `questionable`. Defaults to \'good\' when not specified. |

The `flags` definition could contain only the name property and accept the defaults for the other properties, or explicitly define all the properties. 

For example a Valve could have 2 states, CLOSED or OPEN and accept the defaults, or explicitly define the values. The following Type messages are valid syntax:

	{ 
		"id": "ConfigurationFlags", 
		"flags": {
			"values": [ 
                { "name":"CONFIG_BIT01", "value":1 }, 
                { "name":"CONFIG_BIT02", "value":2 },
                { "name":"CONFIG_BIT03", "value":4 },
                { "name":"CONFIG_BIT04", "value":8 },
                { "name":"CONFIG_BIT05", "value":16 } 
            ] 
		}
	}

    { 
		"id": "ConfigurationFlags",
        "type": integer,
        "format": int16
		"flags": {
			"values": [ 
                { "name":"CONFIG_BIT01", "value":1 }, 
                { "name":"CONFIG_BIT02", "value":2 },
                { "name":"CONFIG_BIT03", "value":4 },
                { "name":"CONFIG_BIT04", "value":8 },
                { "name":"CONFIG_BIT05", "value":16 } 
            ] 
		}
	}
    


# Flags enum Type Messages for Data Quality

The following Type message defines a data quality `flags` where multiple bits (states) can be active at the same time.

An `flags` could be used to define a set of allowed values that represents data quality. In this case include the `quality` in the `flags` values definition. 
If quality is not explicitly set then it is assumed to be \'good\'.

	{ 
		"id": "ConfigurationQualityFlags", 
		"flags": {
			"values": [ 
                { "name":"CONFIG_BIT01", "value":1, "quality": "good" }, 
                { "name":"CONFIG_BIT02", "value":2, "quality": "bad" },
                { "name":"CONFIG_BIT03", "value":4, "quality": "bad" },
                { "name":"CONFIG_BIT04", "value":8, "quality": "questionable" },
                { "name":"CONFIG_BIT05", "value":16, "quality": "questionable" } 
            ] 
		}
	}


When referencing the `flags` enum from the property that holds quality, include the [isquality](xref:typePropertiesAndFormats) keyword and use `reftypeid` as the data type of the property:

    { "DeviceStatus": { "reftypeid": "ConfigurationQualityFlags", "isquality": true } }



### Examples


	[{ 
		"id": "ConfigurationFlags", 
		"flags": {
			"values": [ 
                { "name":"CONFIG_BIT01", "value":1 }, 
                { "name":"CONFIG_BIT02", "value":2 },
                { "name":"CONFIG_BIT03", "value":4 },
                { "name":"CONFIG_BIT04", "value":8 },
                { "name":"CONFIG_BIT05", "value":16 } 
            ] 
		}
	}
	},{ 
		"id": "ConfigurationQualityFlags", 
		"flags": {
			"values": [ 
                { "name":"CONFIG_BIT01", "value":1, "quality": "good" }, 
                { "name":"CONFIG_BIT02", "value":2, "quality": "bad" },
                { "name":"CONFIG_BIT03", "value":4, "quality": "bad" },
                { "name":"CONFIG_BIT04", "value":8, "quality": "questionable" },
                { "name":"CONFIG_BIT05", "value":16, "quality": "questionable" } 
            ] 
		}
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
					"reftypeid": "ConfigurationQualityFlags", 
					"isquality": true
				},
                "ValvePosition": {
                        "reftypeid": "ConfigurationFlags"
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
