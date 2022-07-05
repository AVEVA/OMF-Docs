---
uid: dataMessages
---

# Data Messages

Data messages can be used to create instance data for previously defined Types and Containers, relate instances of static and dynamic data, relate Types, or send type-less static data. Data messages support the following set of actions: `create`, `update` and `delete`.

The body of a Data message is composed of a JSON array with JSON objects defined by the following keywords:

| Name | Value |
| --- | --- |
| `typeid` | Optional ID of the type. If omitted, container or properties is expected. |
| `containerid` | Optional ID of the container. If omitted, type or properties is expected. |
| `properties` | Optional key-value pairs defining the properties of the Type. Used to support sending type-less static data values. |
| `values` | An array of objects conforming to the type. |

For a data message, either the `id` of a previously defined `type` or `container` must be specified, or the data messages must be used to send type-less static data and specify the `properties`.

If `typeid` is specified, the values array must conform to the definition of that Type.

If `containerid` is specified, the values must conform to the Type associated with the Container.

If `properties` is specified, then the data message can be used to send static data for an instance that has no Type.
Optionally a `typeid` may be specified along with the `properties` to extend a `static` Type with additional properties.

If a property is defined on the Type definition, and that property is not included in the `values` array, then a default value for that property will be assumed. Default values are specified
in the [Supported Formats](xref:typePropertiesAndFormats) Table.

If the `action` header value is `delete` then indexed `properties` must be provided. An property is indexed if the `isindexed` keyword is `true` on the Data message Type. Secondary indexes specified on a Container are not required.

## Link Data Messages

[__Link](xref:linkType) Data messages are used to create relationships between static Types, static and dynamic Types, and instance Data.
To define a link relationship, set the `typeid` of the data message to `__Link`, and in the values array specify the `source` and `target` of the link relationship.
Refer to [Link Type](xref:linkType) for detailed information on defining links in data messages to relate data.

## Examples of Data Messages

   - [Link Type](xref:linkType)
   - [Data Example](xref:dataExample)

