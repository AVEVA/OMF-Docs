==========================
Property Types and Formats
==========================

OMF supports extensions to the base set of JSON Schema data types through the ``format`` keyword, as described in the table below.

========   ================  ===========
Type       Format            Description
========   ================  ===========
array                        An array of objects. The ``items`` keyword defines the type of the objects
\                            in the array.
boolean                      A value of either "true" or "false".
integer    int64             64-bit integer.
integer    int32 (default)   32-bit integer.
integer    int16             16-bit integer.
number     double            Double-precision 64-bit floating point.
number     float (default)   Single-precision 32-bit floating point.
number     half              Half-precision 16-bit floating point.
object     dictionary        A dictionary of objects, indexed by a string key. The ``additionalProperties``
\                            keyword defines the dictionary's value type.
string     date-time         A string representation of a timestamp, formatted as YYYY-MM-DDThh:mm:ss.fffZ.
========   ================  ===========


