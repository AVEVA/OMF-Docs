---
uid: typeMessages
---

# Type Messages

Types are used within OMF to define the structure of data. Dynamic types are used by containers to create streams of sequentially indexed data. Static types are used by the endpoint to define non-streamed data, such as assets. Enum types are used to create an array name/value pairs to create a limited set of values for a property in a dynamic or static type. The Type messages are used to create, update and delete types. While types conntain a version, it is informational only. Multiple versions of the same type are not supported.

The body of a Type message consists of an array of objects. The following keywords are used to define a Type.

| Name | Value |
| --- | --- |
| `id` | Unique identifier of the Type. |
| `version` | Optional version of the Type stored as metadata. The version must be of format x.x.x.x, where x must be an integer greater than or equal to 0. If omitted version 1.0.0.0 is assumed. |
| `classification` | One of `dynamic` or `static`. If omitted, the type cannot be directly created, for example enumerations and types composed into other types. |
| `type` | Inherited from JSON Schema. Set to `object` to define a static or dynamic Type. |
| `name` | Optional friendly name for the Type. |
| `description` | Optional description for the Type. |
| `tags` | Optional array of strings to tag the Type. |
| `metadata` | Optional key-value pairs associated with the Type. |
| `enum` | Optional object containing name/value pairs used to define an allowed set of values and optional type and format properties. Classification should not be set when defining an enum Type. |
| `extrapolation` | Optional data mode used to provide consistency when reading values. Supported values include `all`, `none`, `forward`, and `backward`. |
| `properties` | Key-value pairs defining the properties of a static or dynamic Type. Required unless the Type defines enum. |

The `id` cannot begin with the character sequence __. This has been reserved for predefined Types. Currently the only supported predefined Type is [__Link](xref:linkType). The `id` property is referenced when creating instances of Types in Container and Data messages, or when creating other Types that include this Type as a referenced Type.

The `version` is used to supply information about the Type definition and is stored as meta data.

A `static` classification represents metadata describing a device being observed and should be used to capture data that is descriptive and
relatively unchanging. A `dynamic` classification represents observed or calculated measurements taken from a device that update frequently.

If a Type is created for the sole purpose of being referenced by another Type, then `classification` is not required. If classification is not set, then instance data of that type cannot be created.

Type message defined as `enum` defines a set of name/value pairs and is used for properties that have a predefined set of allowed values.
The `enum` type is created separately so that it can be referenced by multiple properties. Refer to [Enum Type](xref:enumType) for detailed information on defining an enum, and using the `reftypeid` to relate the enum property with the enum definition.

The supported data types and data formats for `properties` are documented in the [Type Properties and Formats](xref:typePropertiesAndFormats) topic.

### Examples of Type Messages and Property Formats

   - [Type Properties and Formats](xref:typePropertiesAndFormats)
   - [Enum Type](xref:enumType)
   - [Type Message Example](xref:typeExample)
