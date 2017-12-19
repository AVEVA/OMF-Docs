==========================
Type Properties and Formats
==========================

The following keywords used to define a Type Property:

=================== =============================
Keyword             Description
=================== =============================
isindex   	        At least one Type Property must be designated as the index by supplying the isindex keyword with a value of true. The designated isindex property is used to uniquely identify discrete Data objects so that they can be updated or deleted after their initial creation. For a compound index, the order of index properties within the message determines the order within the index.
isname              One Type Property may be optionally designated as the name by supplying the isname keyword with a value of true. Because the isindex must be unique across all assets, the name keyword allows for multiple distinct Data objects to share a common name.
name                Optional friendly name for the Type Property.
description         Optional description for the Type Property.
=================== =============================

OMF supports the array, boolean, integer, number, and string data types defined by JSON Schema. Timestamps, dictionaries, and bit length-specific numeric properties may also be defined by setting the ``format`` keyword, as described in the table below.

========   =================  ===========
Type       Format             Description
========   =================  ===========
array                         An array of objects. The required ``items`` keyword defines the type of the objects in the array.                           
boolean                       A value of either "true" or "false".
integer    int64              64-bit integer.
integer    int32 (default)    32-bit integer.
integer    int16              16-bit integer.
integer    uint64             64-bit unsigned integer.
integer    uint32             32-bit unsigned integer.
integer    uint16             16-bit unsigned integer.
number     float64            64-bit floating point.
number     float32 (default)  32-bit floating point.
number     float16            16-bit floating point.
object     dictionary         A dictionary of objects, indexed by a string key. The ``additionalProperties`` keyword defines the dictionary's value type.                             
string                        A string.
string     date-time          A string representation of a timestamp, formatted as YYYY-MM-DDThh:mm:ss.fffZ.                            
========   =================  ===========


