---
uid: typePropertiesAndFormats
---

# Type Properties and Formats

The following keywords are used to define a Type Property:

| Name | Value |							
| --- | --- |
| `type` | Required type of the Type Property which must match a type listed in the Supported Formats table below. |
| `format` | Optional format of the `type` Property that, if specified, must be from the table below. |
| `isindex` | At least one Type Property must be designated as the index by supplying the isindex keyword with a value of true. The designated isindex property is used to uniquely identify discrete Data objects so that they can be updated or deleted after their initial creation. For a compound index, the order of index properties within the message determines the order within the index. |
| `isname` | One Type Property may be optionally designated as the name by supplying the isname keyword with a value of true. Because the index must be unique across all Data objects, the isname keyword allows for multiple distinct Data objects to share a common name. |
| `name` | Optional friendly name for the Type Property. |
| `description` | Optional description for the Type Property. |
| `uom` | Optional unit of measure for the Type Property. |

OMF supports the array, boolean, integer, number, and string data types defined by JSON Schema. Timestamps, dictionaries, and bit length-specific numeric properties may also be 
defined by setting the `format` keyword, as described in the Supported Formats table below.

  
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
The datatype and `null` may appear in any order in the array. For example: 

	"MeasurementValue": {"type": ["integer", "null"], "format": "int64"}

	"MeasurementValue": {"type": ["null", "integer"], "format": "int64"}

Values of type "array", "object", and "string" are treated as inherently nullable thus the additional null type specification is not needed.