Link Data Messages
^^^^^^^^^^^^^^^^^^^^^

A Link is a pre-defined type with the typeid ``__Link``. It has the following properties.

The link can be used to create relationships between instances of ``static`` Types, or create a relationship between a ``static`` Type instance and a Container instance.

=================== ======================================
Name                Value
=================== ======================================
``source``			An object representing the source of the link.
``target``			An object representing the target of the link.
=================== ======================================

Each ``source`` and ``target`` object has the following keywords:

=================== ======================================
Name                Value
=================== ======================================
``typeid``          Optional id of the type. If omitted, containerid is expected.
``containerid``     Optional id of the container. If omitted, typeid is expected.
``typeversion``     Optional version of the type to be linked to or from. The version must be of format x.x.x.x, where x must be an integer greater than or equal to 0. If omitted version 1.0.0.0 is assumed.
``index``           Value of the :doc:`isindex <Type_Properties_and_Formats>` property defined when creating the instance of a Type. If typeid is specified, index is required. If containerid is specified index is not supported.
``property``		Optional name of a property defined in the Type definition to be used by the link relationship.
=================== ======================================

Use the __Link typeid in a Data Messages to create relationships between instance data and containers.

To relate to an instance of a type (typically ``static`` data), specify the ``typeid`` and ``index`` of the instance.

To relate to a container, specify only the ``containerid``.  

For example, to relate the instance of a Type Plant, specified by its indexed property PlantId with value WTP1, to the instance of a Type Tank, specified with by its indexed property TankName with value Tank1, use the following __Link:

::

	[{ 
		"typeid": "Plant", 
		"values": [{ "PlantId": "WTP1", "PlantName": "Water Treatment Plant One" }] 
	}, { 
		"typeid": "Tank", 
		"values": [{ "TankName": "Tank1" }] 
	}, { 
		"typeid": "__Link", 
		"values": [{ "source": { "typeid": "Plant", "index": "WTP1"}, 
			"target": { "typeid": "Tank", "index": "Tank1" } }]
	}]
	

To associate the container, Tank1Measurements, with the instance of a Tank whose index is Tank1, use the following __Link:

::

	[{ 	"typeid": "__Link", 
		"values": [{ "source": { "typeid": "Tank", "index": "Tank1"}, 
			"target": {"containerid": "Tank1Measurements"} }]
	}]	
	

If a Type message includes the ``dynamic`` data using the ``reftype`` then the explicit ``__Link`` message is not needed, and the ``containerid`` can be included when creating the Type instance.

For example, if the Tank contains a property with ``reftype`` TankMeasurements, and TankMeasurements is ``dynamic`` then the relationship can be created when the Tank instance is created.

::

	{
		"typeid": "Tank",
		"values": [{ 
			"TankName": "Tank2", 
			"Serial": "2364-4243-FS12", 
			"Model": "TK-421",
			"Measurements": { 
				"containerid": "Tank2Measurements" 
			} 
		}]
	}

