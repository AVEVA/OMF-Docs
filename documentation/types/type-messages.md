---
uid: typeMessages
---

# Type Messages


Types do not support deletes via OMF. The version field is supplied as meta data only. 
Once a Type is deleted, any operations on Containers or Data using that Type will fail.

The body of a Type message consists of an array of objects. The following keywords are used to define a Type.

| Name | Value |
| --- | --- |
| `id` | Unique identifier of the Type. |
| `version` | Optional version of the Type stored as metadata. The version must be of format x.x.x.x, where x must be an integer greater than or equal to 0. If omitted version 1.0.0.0 is assumed. |
| `classification` | One of `dynamic` or `static`. If omitted, the type cannot be directly created, for example enumerations, base types, and types composed into other types. |
| `type` | Inherited from JSON Schema. Set to `object` to define a static or dynamic Type. |
| `basetypeid` | Optional id of a previously defined type. Used to inherit properties for Types of the same classification, or inherit from a Type with no classification. |
| `name` | Optional friendly name for the Type. |
| `description` | Optional description for the Type. |
| `tags` | Optional array of strings to tag the Type. |
| `metadata` | Optional key-value pairs associated with the Type. |
| `enum` | Optional object containing name/value pairs used to define an allowed set of values and optional type and format properties. Classification should not be set when defining an enum Type. |
| `extrapolation` | Optional data mode used to provide consistency when reading values. Supported values include `all`, `none`, `forward`, and `backward`. |
| `properties` | Key-value pairs defining the properties of a static or dynamic Type. Required unless the Type defines enum. |

The `id` cannot begin with the character sequence __. This has been reserved for predefined Types. Currently the only supported predefined Type 
is [__Link](xref:linkType). The `id` property is referenced when creating instances of Types in Container and Data messages, or when 
creating other Types that include this Type as a base type or referenced Type.

The `version` is used to supply information about the Type definition and is stored as meta data. 

A `static` classification represents metadata describing a device being observed and should be used to capture data that is descriptive and
relatively unchanging. A `dynamic` classification represents observed or calculated measurements taken from a device that update frequently. 

The `basetypeid` is used to support Type inheritance and is an `id` of previously defined Type. The properties of the base type are then included in the new Type. Circular inheritance or self-referencing is not supported when using `basetypeid`. 
If a Type is created for the sole purpose of being referenced by another Type, then `classification` is not required. If classification is not set, then instance data of that Type cannot be created.
If the classification is set to `static` or `dynamic` then the classification of each Type must match when using `basetypeid` to define an inheritance relationship.

Type message defined as `enum` defines a set of name/value pairs and is used for properties that have a predefined set of allowed values. 
The `enum` type is created separately so that it can be referenced by multiple properties. Refer to [Enum Type](xref:enumType) for detailed information on defining an enum, and using the `reftypeid` to relate the enum property with the enum definition.

The supported data types and data formats for `properties` are documented in the [Type Properties and Formats](xref:typePropertiesAndFormats) Topic. 

### Examples of Type Messages and Property Formats

   - [Type Properties and Formats](xref:typePropertiesAndFormats)
   - [Enum Type](xref:enumType)
   - [Type Message Example](xref:typeExample)
