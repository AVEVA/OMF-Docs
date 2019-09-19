What's New
==========

Version 1.2 introduces the following incremental changes from version 1.1:

Enhancements for Type messages:
	- Ability to create complex types that combine static and dynamic data, support inheritance and provide reuse with the ``reftype`` keyword defined in the :doc:`Type Properties and Formats <Type_Properties_and_Formats>`. 
	- Support for reusable enumeration sets using the ``enum`` keyword when defining the :doc:`Type Message <Type_Messages>` and the ``reftype`` keword when defining ``properties`` of this enum Type. 
	- Ability to indicate if a data value is `good`, `bad`, or `questionable` using enumeration sets and the ``isquality`` keyword in the :doc:`Type Properties and Formats <Type_Properties_and_Formats>`. 
	- Support for ``minimum`` and ``maximum`` type qualifiers defined in the :doc:`Type Properties and Formats <Type_Properties_and_Formats>`, used to restrict data values.
	- Support for ``interpolation`` and ``extrapolation`` modes defined in the :doc:`Type Properties and Formats <Type_Properties_and_Formats>`, used to describe the  to categorize the type of data being st.


Enhancements for Container messages:
	- Ability to override values of ``properties`` defined by a dynamic Type when creating Containers using the ``propertyoverrides`` keyword in the :doc:`Container Message <Container_Messages>`. Currently supported property overrides include ``name``, ``description``, ``uom``, ``minimum``, and ``maximum``.
	- Ability to set the source of a stream of data for a :doc:`Container <Container_Messages>` by specifying the ``datasource`` keyword in the ``metadata`` of the container.


Enhancements for Data messages:
	- Ability to relate instances of static and dynamic data without explicitly creating a ``__Link`` relationship and when using complex Type definitions.  


