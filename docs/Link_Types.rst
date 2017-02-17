Links
^^^^^

A Type with Link classification must declare the following additional properties:

=================== =============================
Name                Value
=================== =============================
``source0-N``   	Objects describing the sources of the link
``target0-N``       Objects describing the targets of the link
=================== =============================

The number of sources and targets may vary and must be marked source0, source1, ..., sourceN, target0, target1, ..., targetN. The objects in the source and targets consist of the following properties:  

=================== =============================
Name                Value
=================== =============================
``linktype``   	    Type to be linked to or from.
``linktypeversion`` Optional version of the type to be linked to or from. If omitted version 1.0.0.0 is assumed.
=================== =============================