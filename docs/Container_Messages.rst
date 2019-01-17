Container Messages
------------------

A Container is defined as a collection of Data events of identical Type and version. Each Container has a unique ID, defined upon creation of the Container.

Once a Type has been registered with a Type message, Containers can begin using that Type. Containers can be created, updated, or deleted.

The body of a Container message consists of an array of objects with the following keywords:

=====================  =================================================================================================
Name                   Value
=====================  =================================================================================================
``id``                 Unique identifier of the Container.
``typeid``             ID of the Type used by the Container.
``action``             Optional: One of: ``create``, ``update``, or ``delete``. The value specified overrides the value of the ``action`` header. If omitted, the value of the ``action`` header is assumed. See :doc:`Headers`.
``description``        Optional description for the Container.
``indexes``            Optional array of Type Property ids to be used as secondary indexes for the Container.
``metadata``           Optional key-value pairs associated with the Container.
``name`` 	           Optional friendly name for the Container.
``propertyoverrides``  Optional key-value pairs defining overrides to properties of the Type.
``tags``               Optional array of strings to tag the Container.
``typeversion``        Optional version of the Type used by the Container. The version must be of format x.x.x.x, where x must be an integer greater than or equal to 0. If omitted, version 1.0.0.0 is used.
``datasource``         Optional string to identify the source of data.
=====================  =================================================================================================

Some keywords of Type properties may be overriden on a container level with the help of the optional ``propertyoverrides`` keyword. The value definition is the same as for the ``properties`` keyword of :doc:`Types <Type_Messages>`, but overrides can only be used on ``name``, ``description``, and ``uom`` keywords of Type Properties. The complete list of Type Property keywords can be found :doc:`here <Type_Properties_and_Formats>`.


.. toctree::

      Container_Msg_Sample
