Group Messages
---------------

A Group is defined as a collection of data events of identical Type. Each Group has a unique ID, defined upon creation of the Group.

Once a Type has been registered with a Type message, Groups can begin using that Type. Groups can be created, updated, or deleted.

The body of a Group message consists of an array of objects made up of the following properties:

=============== =================================================================================================
Name            Value
=============== =================================================================================================
``id``          Unique identifier of the Group.
``type``        ID of the Type used by the Group.
``typeversion`` Optional version of the Type used by the Group. If omitted, version 1.0.0.0 is used.
``name`` 	    Optional friendly name for the Group.
``description`` Optional description for the Group.
``tags``        Optional array of strings to tag the Group.
``metadata``    Optional key-value pairs associated with the Group.
=============== =================================================================================================

.. toctree::

      Group_Msg_Sample
