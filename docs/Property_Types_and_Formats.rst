==========================
Property Types and Formats
==========================

OMF supports the array, boolean, integer, number, and string data types defined by JSON Schema. Timestamps, dictionaries, and bit length-specific numeric properties may also be defined by setting the ``format`` keyword, as described in the table below.

========   =================  ===========
Type       Format             Description
========   =================  ===========
array                         An array of objects. The ``items`` keyword defines the type of the objects
\                             in the array.
boolean                       A value of either "true" or "false".
integer    int64              64-bit integer.
integer    int32 (default)    32-bit integer.
integer    int16              16-bit integer.
number     float64            64-bit floating point.
number     float32 (default)  32-bit floating point.
number     float16            16-bit floating point.
object     dictionary         A dictionary of objects, indexed by a string key. The ``additionalProperties``
\                             keyword defines the dictionary's value type.
string                        A string.
string     date-time          A string representation of a timestamp, formatted as
\                             YYYY-MM-DDThh:mm:ss.fffZ.
========   =================  ===========


