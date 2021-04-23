---
uid: typePropertiesAndFormats
---

# Type Properties and Formats

The following keywords are used to the define the `properties` in the Type definition:

| Name | Value |							
| --- | --- |
| `type` | Type of the Property. Must match a type listed in the \'Supported Formats\' table below. Either `type` or `reftypeid` is required for each property. |
| `format` | Optional format of the `type` Property that, if specified, must be from the \'Supported Formats\' table below. |
| `reftypeid` | `id` to a previously defined Type. Either `type` or `reftypeid` is required for each property. |
| `isindex` | At least one Type Property must be designated as the index, or the Type cannot be used to create instance data. The designated isindex boolean property is used to uniquely identify discrete Data objects so that they can be updated or deleted after their initial creation. For a compound index, the order of index properties within the message determines the order within the index. |
| `isname` | One Type Property may optionally be designated as the name by specifying a boolean value of true. Because the index must be unique across all Data objects, the isname keyword allows for multiple distinct Data objects to share a common name. |
| `isquality` | One or more type Properties may optionally be designated as quality. These properties would then determine the overall quality of each data value. Properties designated as quality can be of any supported type and format or represented by enums or flags. |
| `name` | Optional friendly name for the Type Property. This property can be overridden using the propertyoverrides keyword on a Container message. |
| `description` | Optional description for the Type Property. This property can be overridden using the propertyoverrides keyword on a Container message. |
| `uom` | Optional unit of measure for the Type Property. This property can be overridden using the propertyoverrides keyword on a Container message. |
| `minimum` | Optional type qualifier that defines minimum allowed value. This property can be overridden using the propertyoverrides keyword on a Container message. This property is only valid on numbers and integers. |
| `maximum` | Optional type qualifier that defines maximum allowed value. This property can be overridden using the propertyoverrides keyword on a Container message. This property is only valid on numbers and integers. |
| `interpolation` | Optional data mode used to provide consistency when reading data. Supported values include `continuous`, `discrete`, `stepwisecontinuousleading`, and `stepwisecontinuousfollowing`. |
| `extrapolation` | Optional data mode used to provide consistency when reading values. Supported values include `all`, `none`, `forward`, and `backward`. |

For each property, `type` or `reftypeid` must be defined. When using `type` refer to the \'Supported Formats\' table below for the list of allowed values.
When using `reftypeid`, the value must be set to the `id` of a previously defined Type. Circular inheritance or self-referencing is not supported when using `reftypeid`. 

If `type` is used, the format of the type may be set using the `format` keyword, as described in the \'Supported Formats\' table below. 
This allows for the creation of timestamps, dictionaries, and bit length-specific numeric properties.

If `reftypeid` is used, set the value to the `id` of a previously defined Type. 
If the referenced type is an `enum` then it defines the allowed set of data values for this property.
If the referenced type is a `static` or `dynamic` Type, then the properties of that Type are included as child properties of this property. 


### Supported Formats

| Type | Format | Default Value | Description |
| --- | --- | --- | --- |
| array | null | An array of objects. The required `items` keyword defines the type of the objects in the array. |                        
| boolean | | false | A value of either "true" or "false". |
| integer | int64 | 0 | 64-bit integer. |
| integer | int32 (default) | 0 | 32-bit integer. |
| integer | int16 | 0 | 16-bit integer. |
| integer | uint64 | 0 | 64-bit unsigned integer. |
| integer | uint32 | 0 | 32-bit unsigned integer. |
| integer | uint16 | 0 | 16-bit unsigned integer. |
| number | float64 | 0 | 64-bit floating point. |
| number | float32 (default) | 0 | 32-bit floating point. |
| number | float16 | 0 | 16-bit floating point. |
| object | dictionary | null | A dictionary of objects, indexed by a string key. The `additionalProperties` keyword defines the dictionary\'s value type. |                       
| string | | null | A string. |
| string | date-time | 0001-01-01T00:00:00Z | A string representation of a timestamp, formatted as YYYY-MM-DDThh:mm:ssZ, with optional subsecond precision. |                   



### Nullable type properties

Nullable type properties are supported by specifying an array that defines the datatype and includes the keyword `null`. 
The datatype and `null` may appear in any order in the array. The default value for any nullable type is null. For example: 

	"MeasurementValue": { "type": ["integer", "null"], "format": "int64" }

	"MeasurementValue": { "type": ["null", "integer"], "format": "int64" }
	
Values of type "string" are treated as inherently nullable thus the additional null type specification is not needed.
	
### Type reuse and Inheritance

Type reuse and Type inheritance are supported for Types of the same `classification` or Types with no `classification`, using either `basetypeid` on a Type Message, or
`reftypeid` at the Property level. When `basetypeid` is used on a Type, then all the properties of the base type are included within the new Type.
When `reftypeid` is used on a property, then all the properties of the reference type are included under the specified property.


In the example below, `basetypeid` is used to create the new \'CylindricalTank\' Type which will have all the properties of the existing \'Tank\' Type, maintain the index and name properties, 
plus adds an additional property \'TankDiameter\'.

	{
		"id": "Tank",
		"type": "object",
		"classification": "static",		
		"properties": {
			"TankName": { "type": "string", "isname": true,  "isindex": true },
			"Serial": { "type": "string" },
			"Model": { "type": "string" }
		}
	}, {
		"id":"CylindricalTank",
		"type": "object",
		"classification": "static",
		"basetypeid": "Tank",
		"properties": {					
			"TankDiameter": { "type": "number", "format": "float32" }
		}	
	}

In the example below, a reusable type \'LocationProperties\' is created then used with the \'TankV2\' definition via the `reftypeid` to define a Location property on a Tank.  
The TankV2 Location property will contain the sub properties \'Latitude\' and \'Longitude\'.

The referenced type \'LocationProperties\' does not define a classification, and does not define an index property and therefore \'LocationProperties\' cannot be used as the Type for instance data.

	{ 	
		"id":"LocationProperties",
		"type":"object",		
		"properties": { 
			"Latitude":{ "type": "number", "format": "float32" },
			"Longitude":{ "type": "number", "format": "float32" }
		}
	}, {
		"id":"TankV2",
		"type":"object",
		"classification":"static",
		"properties": { 
			"TankName": { "type": "string", "isname": true,  "isindex": true },
			"Serial": { "type": "string" },
			"Model": { "type": "string" },
			"Location": { "reftypeid":"LocationProperties" }	
		}
	}

### Type Qualifiers

Properties with `isindex` keyword designate that property as the index and must have unique values. The index value is set when creating instances of the Type, and referenced when creating links.
Typically, the properties of a `dynamic` type index on time, and use the format `date-time`, and properties of a `static` type index on id or name.
Types without an index property cannot be used to create instance data.

### Data Quality

The `isquality` keyword is used to designate particular property or properties as data quality for the Type. Properties marked with the quality flag should have a reference to an `enum` or `flags` type or be of any supported Types and Formats. In the example below, `isquality` keyword is used in case of property referencing an enumeration set and int16 property. This allows for capturing data quality information in its raw form.

	"DeviceStatus": { "reftypeid": "DeviceStatusEnum", "isquality": true }

	"DeviceStatus": { "type": "Integer", "format": "int16", "isquality": true }

