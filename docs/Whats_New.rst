What's New
==========

Version 1.2-alpha3 introduces the following incremental changes from version 1.1:

- :doc:`Container-level overrides <Container_Messages>` of Type properties using the ``propertyoverrides`` keyword. 
- An ``isquality`` keyword for :doc:`Type properties <Type_Properties_and_Formats>` representing data quality. An additional ``qualityscheme`` keyword specifies the expected scheme.
- Clarification of the expected format for versions used throughout the specification.
- Ability to override CRUD mode at the object-level (:doc:`Type <Type_Messages>`, :doc:`Container <Container_Messages>`, or :doc:`Data <Data_Messages>`) using the ``action`` keyword.
- Addition of the ``patch`` mode to the ``action`` keyword to allow :doc:`partial updates <Data_Messages>` in Data messages.

