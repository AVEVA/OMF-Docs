Types
^^^^^
Every stream creation message must be accompanied by a type definition, to which all of the stream’s data objects must conform. Types are defined using the JSON Schema specification (http://json-schema.org/). 

One property must be designated as the index by supplying the ``index`` keyword with a value of ``true``.

The ``id`` keyword is required, and is used when creating a stream to bind that stream to a given data type.

The ``classification`` keyword is used to denote whether the type is to be used with a Value, Asset, Span, or Link stream. If omitted, the type is assumed to be used with Value streams.

An optional version keyword allows for multiple versions of the same type. If the version keyword is omitted, the version is assumed to be 1.0.0.0. Once a type has been defined, the type’s ``id`` cannot be reused unless a new version is specified.

Depending on the streamtype, additional properties are required:

================= =============================
Stream Type       Required Properties
================= =============================
Span              * ``StartTime``           
                  * ``EndTime``
Link              * ``Source``
                  * ``Target0`` ... ``TargetN``
================= =============================

.. toctree::

   Value_Type_Sample
   Asset_Type_Sample
   Span_Type_Sample
   Link_Type_Sample
