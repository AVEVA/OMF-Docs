Link Messages
^^^^^^^^^^^^^^^^

A Link is a pre-defined type with the typeid __Link. It has the following properties.

=================== ======================================
Name                Value
=================== ======================================
``source``			An object representing the source of the link
``target``			An object representing the target of the link
=================== ======================================

Each ``source`` and ``target`` object has the following keywords:

=================== ======================================
Name                Value
=================== ======================================
``typeid``          Optional id of the type. If omitted, 
                    containerid is expected.
``containerid``     Optional id of the container. If 
                    omitted, typeid is expected.
``typeversion``     Optional version of the type to be 
                    linked to or from. The version must be of format x.x.x.x, where x must be an integer greater than or equal to 0. If omitted 
                    version 1.0.0.0 is assumed.
``index``           Value of the :doc:`Indexed <Type_Properties_and_Formats>` property defined in the instance. If typeid is specified, index is mandatory. If containerid is specified it is optional.
``property``		Optional name of a property defined in the Type definition to be used by the link relationship.
=================== ======================================

The link relationship can be used to link instances of Types, or link instances of a Type and Container. 

When linking instances of Types, a parent child relationship is created for the specified index values. 
If ``typeid`` is specified, then include the ``index``, and optionally specify the ``property`` from the Type definition to be used for the link.

When linking instancs of a Type and a Container, a relationship between Type properties and Container Streams is created. 
If ``containerid`` is specified without an ``index``, the link is for the container.
If ``containerid`` is specified with an ``index``, the link is for a particular container value. 


Link Examples
--------------------

.. toctree::

	Link_Type_Sample
	Link_Container_Sample