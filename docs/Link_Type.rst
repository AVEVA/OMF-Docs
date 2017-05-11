Link Type
^^^^^^^^^

A Link is a pre-defined type with the typeid __Link. It has the following properties.

=================== =============================
Name                Value
=================== =============================
``source``   	    An object representing the source of the link
``target``          An object representing the target of the link
=================== =============================

Each ``source`` and ``target`` object has the following keywords:

=================== ======================================
Name                Value
=================== ======================================
``typeid``   	      Optional id of the type. If omitted, 
                    group is expected.
``containerid``     Optional id of the container. If 
                    omitted, type is expected.
``typeversion``     Optional version of the type to be 
                    linked to or from. If omitted 
                    version 1.0.0.0 is assumed.
``index``           Index of either the data. If typeid 
                    is specified, index is mandatory. 
                    If containerid is specified it is 
                    optional.
=================== ======================================

If ``typeid`` and ``index`` are specified, the link is for a particular non-container value. If ``containerid`` is specified with an ``index``, the link is for a particular container value. If ``containerid`` is specified without an ``index``, the link is for a container.
