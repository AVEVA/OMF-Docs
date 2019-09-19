==============================
Type Properties and Formats
==============================

The following keywords are used to the define the ``properties`` in the Type defintion:

=================== =============================
Name                Value
=================== =============================
``type``                Required type of the Type Property which must match a type listed in the Supported Formats table below, or the isref keyword must be specified.
``format``              Optional format of the Type Propety that, if specified, must be from the table below.
``reftype``             Optional ``id`` to a previously defined Type. When specified, the ``type`` must be set to ``object``. 
``refversion``			Optional version of the ``reftype`` Type definition. The version must be of format x.x.x.x, where x must be an integer greater than or equal to 0. If omitted, the current version of the referenced type will be used. 
``isindex``   	        At least one Type Property must be designated as the index by supplying the isindex keyword with a value of true. The designated isindex property is used to uniquely identify discrete Data objects so that they can be updated or deleted after their initial creation. For a compound index, the order of index properties within the message determines the order within the index.
``isname``              One Type Property may be optionally designated as the name by supplying the isname keyword with a value of true. Because the index must be unique across all Data objects, the isname keyword allows for multiple distinct Data objects to share a common name.
``isquality``			One Type Property may be optionally designated as the Quality by supplying the isquality keyword with a value of true. The designated isquality property is used to determine if the collection of data values has the status `good`, `bad` or `questionable`.
``name``                Optional friendly name for the Type Property. This property can be overridden using the ``propertyoverrides`` keyword on a Container message. 
``description``         Optional description for the Type Property. This property can be overridden using the ``propertyoverrides`` keyword on a Container message. 
``uom``					Optional unit of measure for the Type Property. This property can be overridden using the ``propertyoverrides`` keyword on a Container message. 
``minimum``				Optional type qualifier that defines minimum allowed value. This property can be overridden using the ``propertyoverrides`` keyword on a Container message. 
``maximum``				Optional type qualifier that defines maximum allowed value. This property can be overridden using the ``propertyoverrides`` keyword on a Container message. 				
``interpolation``		Optional data mode used to provide consistency when reading values.
``extrapolation``		Optional data mode used to provide consistency when reading values.
=================== =============================


The ``type`` property must be set to a valid JSON type as defined by JSON Schema. The supported types include string, integer, number, object, boolean, and array. 

The format of the ``type`` may be set using the ``format`` keyword, as described in the Supported Formats table below. This allows for the creation of timestamps, dictionaries, and bit length-specific numeric properties.
  
  
Supported Formats
-----------------

========   =================  	======================  ===========
Type       Format             	Default Value           Description
========   =================	======================  ===========
array                           null                    An array of objects. The required ``items`` keyword defines the type of the objects in the array.                           
boolean                         false                   A value of either "true" or "false".
integer    int64                0                       64-bit integer.
integer    int32 (default)      0                       32-bit integer.
integer    int16                0                       16-bit integer.
integer    uint64               0                       64-bit unsigned integer.
integer    uint32               0                       32-bit unsigned integer.
integer    uint16               0                       16-bit unsigned integer.
number     float64              0                       64-bit floating point.
number     float32 (default)    0                       32-bit floating point.
number     float16              0                       16-bit floating point.
object     dictionary           null                    A dictionary of objects, indexed by a string key. The ``additionalProperties`` keyword defines the dictionary's value type.                             
string                          null                    A string.
string     date-time            0001-01-01T00:00:00Z    A string representation of a timestamp, formatted as YYYY-MM-DDThh:mm:ssZ, with optional subsecond precision.                        
========   =================    ======================  ===========



Nullable type properties: 

Nullable type properties are supported by specifying an array that defines the datatype and includes the keyword ``null``. 
The data type and ``null`` may appear in any order in the array. For example: 

::

	"MeasurementValue": {"type": ["integer", "null"], "format": "int64"}
	
::

	"MeasurementTimestamp": {"type": ["null", "string"], "format": "date-time"}
	


	
Complex types, inheritance and reuse:


Complex type defintions can be created by using the ``reftype`` keyword, and setting the value to the ``id`` of a previously defined Type. When ``reftype`` is set on a property, then that properites ``type`` must be set to ``object``.	

::

	"Measurements": { "type":"object", "reftype":"TankMeasurement" }


Type Qualifiers:

Properties with ``isindex`` keyword must be of type String. 
Properties of a ``dynamic`` type with the ``isindex`` keyword must also include the ``format`` and be set to the value ``date-time``. 
Properties with the ``isname`` keyword must be of type String.

The ``isquality`` keyword is used to designate a particular property as the data quality. When set the type can either be a ``boolean`` or a reference to an enumeration set previously defined by :doc:`enum<Type_Messages>`.
The following formats are supported:
	
::

	"Quality": { "type":"boolean", "isquality": true }

::

	"Quality": { "type":"object", "reftype":"DataQuality", "isquality": true }	
   