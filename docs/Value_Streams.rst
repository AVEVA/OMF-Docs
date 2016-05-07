Value Streams
^^^^^^^^^^^^^
Value streams are designed to represent observed or calculated measurements taken from devices. 
Data objects sent to an on-premises PI system must define an index property of timestamp type. Each additional property of the object is then mapped to a PI point and timestamped with the designated index.
When sending data objects to cloud-hosted Qi system, the index attribute may be of any type. Each attribute defined in the stream type is collated into a single Qi stream, rather than split into multiple streams or points.
