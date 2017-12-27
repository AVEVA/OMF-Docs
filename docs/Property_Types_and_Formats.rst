==========================
Property Types and Formats
==========================

OMF supports the array, boolean, integer, number, and string data types defined by JSON Schema. Timestamps, dictionaries, and bit length-specific numeric properties may also be defined by setting the ``format`` keyword, as described in the table below.

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
string     date-time            0 UTC, January 1, 0001  A string representation of a timestamp, formatted as YYYY-MM-DDThh:mm:ss.fffZ.                            
========   =================    ======================  ===========


