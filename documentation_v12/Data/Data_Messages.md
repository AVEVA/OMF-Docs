---
uid: dataMessages
---

# Data Messages

Data messages are used to create instance data for previously defined Types and Containers, relate instances of static and dynamic data, and relate Types. 
 
The body of a Data message is composed of a JSON array with JSON objects defined by the following keywords: 

| Name | Value |
| --- | --- |
| `typeid` | Optional ID of the type. If omitted, container is expected. |
| `containerid` | Optional ID of the container. If omitted, type is expected. |
| `properties` | Optional key-value pairs defining the properties for type-less static data values. |
| `values` | An array of objects conforming to the type. |

For each object, either `typeid`, `containerid`, or `properties` must be specified. 
If `typeid` is specified, the values array must conform to the definition of that Type. 
If `containerid` is specified, the values must conform to the Type associated with the Container.
If `properties` is specified, then optionally a `typeid` may also be specified. This format is used to either extend a `static` Type, or send static data for an instance that has no Type.

If the data message is used to define a relationship then `typeid` is specified with the value [__Link](xref:linkType).

If a Type Property is defined but no property value is provided in the Data message, a default value will be assumed. Default values are specified 
in the [Supported Formats](xref:typePropertiesAndFormats) Table.

	
### Link Data Messages

[__Link](xref:linkType) messages are used to create relationships between static Types, static and dynamic Types, and instance Data.
To define a link relationship, set the `typeid` of the data message to `__Link`, and in the values array specify the `source` and `target` of the link relationship. 
Refer to [Link Type](xref:linkType) for detailed information on defining links in data messages to relate data. 

### Examples of Data Messages 

   - [Link Type](xref:linkType)
   - [Data Example](xref:dataExample)


