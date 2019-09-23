Message Types
=============

Messages are defined using the JSON Schema specification (http://json-schema.org/). 	
Each message is a JSON Array containing one or more JSON objects. 

The OMF ``messagetype`` specified in the header describes the type of data in the JSON array, and must be set to one of the following categories: ``type``, ``container``, or ``data``. 
For each OMF ``messagetype``, the ``action`` to take on the message body is one of ``create``, ``update``, or ``delete``. If not explicitly set then the ``action`` will default to ``create``.

Refer to the following topics for detailed information on the supported formats of each ``messagetype``:
	- :doc:`Type Messages <Type_Messages>`
	- :doc:`Container Messages <Container_Messages>`
	- :doc:`Data Messages <Data_Messages>`

For a complete working example of Type, Container and Data messages refer to the following example:
	- :doc:`OMF v1.2 Example<OMF_Msg_Sample>`

To achieve optimal throughput, include multiple messages of the same ``messagetype`` within the JSON array, and apply ``compression`` to the message body as described in the :doc:`Headers<Headers>` Topic.  


