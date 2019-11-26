---
uid: messageTypes
---

# Message Types

Messages are defined based on the concepts in the JSON Schema specification (http://json-schema.org/). 	
Each message is a JSON Array containing one or more JSON objects. 

The OMF `messagetype` specified in the message header describes the type of data in the JSON array. The `messagetype` must be set to one of the following categories: `type`, `container`, or `data`.
Refer to the following topics for detailed information on the supported formats of each `messagetype`:

- [Type](xref:typeMessages)
- [Container](xref:containerMessages)
- [Data](xref:dataMessages)


For each OMF `messagetype`, the `action` to take on the message body is one of 	`create`, `update`, or `delete`.  
If not explicitly set then the `action` will default to `create`.


For a complete working example of Type, Container and Data messages refer to the following example:
- [OMF v1.2 Example](xref:OMFMsgSample)

To achieve optimal throughput, include multiple messages of the same `messagetype` within the JSON array, and apply `compression` to the message body as described in the [Message Headers](xref:headers) Topic. 