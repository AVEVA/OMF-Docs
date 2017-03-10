Container Messages
------------------

A Container is defined as a collection of Data events of identical Type and version. Each Container has a unique ID, defined upon creation of the Container.

Once a Type has been registered with a Type message, Containers can begin using that Type. Containers can be created, updated, or deleted.

The body of a Container message consists of an array of objects with the following keywords:

=============== =================================================================================================
Name            Value
=============== =================================================================================================
``id``          Unique identifier of the Container.
``typeid``        ID of the Type used by the Container.
``typeversion`` Optional version of the Type used by the Container. If omitted, version 1.0.0.0 is used.
``name`` 	    Optional friendly name for the Container.
``description`` Optional description for the Container.
``tags``        Optional array of strings to tag the Container.
``metadata``    Optional key-value pairs associated with the Container.
=============== =================================================================================================

.. toctree::

      Container_Msg_Sample
