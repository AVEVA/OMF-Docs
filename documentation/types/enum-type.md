---
uid: enumType
---

# Enum Type Message
An `enum` is a type message defined by an array of name/value pairs used to create a limited set of allowed values. Once defined, the `enum` can be referenced by Properties within other Type messages.

An `enum` can also be used to define a set of Data Quality values and referenced from property marked as `isquality`.

## Enum Type Properties
The following keywords are used to define `enum` type definition. If a keyword is not specified the default will be used.

| Name | Value |
| --- | --- |
| `type` | Optional type of the enum. The only currently supported type is integer. Default: integer |
| `format` | Optional format of the type property. Must be from the OMF 1.2 'supported' formats table. Default: int16 |
| `values` | Required array of name/value pairs used to create a limited set of allowed values. |

## Enum values collection keywords
To define possible values of an `enum` type, include the following keywords. If a keyword is not specified the default will be used.

| Name | Value |
| --- | --- |
| `name` | Required unique string that describes the condition or state being represented. This string is used as the displayed value when an enum is selected as the Type for a property. |
| `value` | Required unique integer value associated with the enum. The integer value must be used when sending data for container properties of this type. |

In this example we have a Valve with 2 states, CLOSED or OPEN and accept the defaults, or explicitly define the values. The following Type messages are valid syntax:

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

	{
		"id": "ValveState",
		"enum": {
			"type": "integer",
        		"format": "int16",
			"values":[ { "value":0, "name":"CLOSED" }, { "value":1, "name":"OPEN" } ]
		}
	}

## Enum Type Messages for Data Quality

An `enum` could be used to define a set of allowed values that represents data quality.

When referencing the `enum` type from the property that holds quality, include the [isquality](xref:typePropertiesAndFormats) keyword and use `reftypeid` as the data type of the property:

    { "DeviceStatus": { "reftypeid": "DeviceStatusEnum", "isquality": true } }

## Remarks
 - Properties referencing `enum` type must send integer values in a data message; the use of strings is unsupported.
 - `enum` types can be defined as non-continuous sets.

## Examples

	[{
		"id": "ValveState",
		"version": "1.0.0.0",
		"enum": {
			"values": [ { "name":"CLOSED", "value":0 }, { "name":"OPEN", "value":1 } ]
		}
	}, {
		"id": "DeviceStatusEnum",
		"enum": {
			"values": [
				{ "name": "Device Connected", "value": 0 },
				{ "name": "Device Failure", "value": 1 },
				{ "name": "Device Comm Failure", "value": 2 },
				{ "name": "Uncertain Out Limits", "value": 3 } ]
			}
	}, {
		"id": "TankMeasurementV1",
		"version": "1.0.0.0",
		"type": "object",
		"classification": "dynamic",
		"extrapolation": "forward",
		"properties": {
			"Timestamp": {
				"type": "string",
				"format":"date-time",
				"isindex": true
			},
			"DeviceStatus": {
				"reftypeid": "DeviceStatusEnum",
				"isquality": true,
				"interpolation": "stepwisecontinuousleading"
			},
			"ValvePosition": {
				"reftypeid": "ValveState",
				"interpolation": "stepwisecontinuousleading",
			},
			"Pressure": {
				"type": "number",
				"name": "Tank Pressure",
				"description": "Tank Pressure in Pa",
				"uom": "pascal",
				"interpolation": "continuous"
			},
			"Temperature": {
				"type": "number",
				"name": "Tank Temperature",
				"description": "Tank Temperature in K",
				"uom": "K",
				"interpolation": "continuous"
			}
		}
	}]
