---
uid: enumFlagsType
---

# Enum and Flags Type Messages

## Enum Type Message
An `enum` is a Type message defined using an array of name/value pairs used to create a limited set of allowed values. Once defined, the `enum` can be referenced by Properties within other Type messages.

An `enum` can also be used to define a a set of Data Quality values. When defining data quality include the `quality` property in the enum definition, and denote the quality as `good`, `bad`, or `questionable`.

### Enum Type Properties
The following keywords are used to define Enum Type definition.

| Name | Value |
| --- | --- |
| `type` | Optional type of the enum. The only currently supported type is integer. Default: integer |
| `format` | Optional format of the type property. Must be from the OMF 1.2 'supported' formats table. Default: int16 |
| `values` | Array of name/value pairs used to create a limited set of allowed values. When enum is used to define a set of Data Quality values quality property can be included to denote the quality as good, bad, or questionable. |

### Enum values collection keywords
To define possible values of an `enum` type, include the following keywords. If a keyword is not specified the default is going to be used.

| Name | Value |
| --- | --- |
| `name` | A unique string that describes the condition or state being represented. This string is used as the displayed value when an enum is selected as the Type for a property. |
| `value` | Optional integer value associated with the enum. If not defined the enum ranges from 0 to one less than size of the collection. The integer value is typically used when sending data of this type. |
| `quality` | Optional field needed when defining a set of data quality values. Must be set to `good`, `bad`, or `questionable`. Defaults to \'good\' when not specified. |

The `enum` definition could contain only the name property and accept the defaults for the other properties, or explicitly define all the properties. 

For example a Valve could have 2 states, CLOSED or OPEN and accept the defaults, or explicitly define the values. The following Type messages are valid syntax:
```json
	{ 
		"id": "ValveState", 
		"enum": {
			"values":[ "CLOSED", "OPEN"]
		}
	}

	{ 
		"id": "ValveState", 
		"enum": {
			"values": [ { "name":"CLOSED", "value":0 }, { "name":"OPEN", "value":1 } ] 
		}
	}
	
	{ 
		"id": "ValveState", 
		"enum": {
			"values":[ { "value":0, "name":"CLOSED" }, { "value":1, "name":"OPEN" } ] 
		}
	}
```

## Enum Type Messages for Data Quality

The following Type message defines a data quality `enum`.

An `enum` could be used to define a set of allowed values that represents data quality. In this case include the `quality` in the `enum` definition. 
If quality is not explicitly set then it is assumed to be \'good\'.

```json
	{ 
		"id": "DeviceStatusEnum", 
		"enum": {
			"values": [ 
				{ "name": "Device Connected", "value": 0 },
				{ "name": "Device Failure", "value": 1, "quality": "bad" },
				{ "name": "Device Comm Failure", "value": 2, "quality": "bad" },
				{ "name": "Uncertain Out Limits", "value": 3, "quality": "questionable" } 
			]
		}
	}
```

When referencing the `enum` from the property that holds quality, include the [isquality](xref:typePropertiesAndFormats) keyword and use `reftypeid` as the data type of the property:

```json
    { "DeviceStatus": { "reftypeid": "DeviceStatusEnum", "isquality": true } }
```

## Flags Type Messages

A `flag` enum is a Type message defined using an array of name/value pairs used to create a limited set of allowed values where multiple states (bits) can be active at the same time. Once defined, the `flags` enum can be referenced by Properties within other Type messages.

### Flags Type Properties

The following keywords are used to define Flags Type definition.

| Name | Value |
| --- | --- |
| `type` | Optional type of the Flags definition. The only currently supported type is integer. Default: integer |
| `format` | Optional format of the type property. Defines how many flags can be defined in the values array. Must be from the OMF 1.2 'supported' formats table. Default: int32 |
| `values` | Array of name/value pairs used to create a limited set of allowed values. When enum is used to define a set of Data Quality values quality property can be included to denote the quality as good, bad, or questionable. |

### Flags values collection keywords
To define possible values of a `flags` type, include the following keywords. If a keyword is not specified the default is going to be used.

| Name | Value |
| --- | --- |
| `name` | A unique string that describes the condition or state being represented. |
| `value` | Required integer value associated with the given state (bit). |
| `quality` | Optional field needed when defining a set of data quality values. Must be set to `good`, `bad`, or `questionable`. Defaults to \'good\' when not specified. |

The example below shows 'flags' type definition describing various configuration bits where multiple can be set at the same time.

```json
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
```

## Flags Type Messages for Data Quality

The following Type message defines a data quality `flags` where multiple states (bits) can be active at the same time.

A `flags` type could be used to define a set of allowed values that represents data quality. In this case include the `quality` in the `flags` values definition. 
If quality is not explicitly set then it is assumed to be \'good\'. Flags can combine multiple states with different quality mappings set:
 - When at least one flag with bad quality is set the value is considered bad.
 - When at least one flag with questionable quality is set the value is considered questionable.
 - Combination of Bad and Questionable flags is not allowed. When bad and questionable bits are combined the value is considered bad and questionable bit will not be set.

 ```json
	{ 
		"id": "ConfigurationQualityFlags", 
		"flags": {
			"values": [ 
                { "name":"Good", "value":1 }, 
                { "name":"Uninitialized", "value":2, "quality": "bad" },
                { "name":"Unreasonable", "value":4, "quality": "bad" },
                { "name":"Suspect", "value":8, "quality": "questionable" },
                { "name":"Commanded", "value":16 } 
            ] 
		}
	}
```

When referencing the `flags` enum from the property that holds quality, include the [isquality](xref:typePropertiesAndFormats) keyword and use `reftypeid` as the data type of the property:

```
    { "DeviceStatus": { "reftypeid": "ConfigurationQualityFlags", "isquality": true } }
```

## Remarks
Properties referencing `flags` or `enum` type must send integers in a data message, since use of strings is unsupported.


## Examples

```json
	[{
        "id": "ValveState",
        "version": "1.0.0.0",        
        "enum": {
			"values": [ {"name":"CLOSED", "value":0}, {"name":"OPEN", "value":1} ]
		}
	}, { 
        "id": "DeviceStatusEnum", 
		"enum": {
			"values": [ 
				{ "name": "Device Connected", "value": 0, "quality": "good" },
				{ "name": "Device Failure", "value": 1, "quality": "bad" },
				{ "name": "Device Comm Failure", "value": 2, "quality": "bad" },
				{ "name": "Uncertain Out Limits", "value": 3, "quality": "questionable" } 
			]
		}
    },
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
                },
				"Configuration": {
						"reftypeid": "ConfigurationFlags"
				}
        }
	}]
	```