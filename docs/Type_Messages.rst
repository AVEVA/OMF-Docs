===============
 Type Messages
===============
Each Stream, Span, Asset, and Link must be associated with a Type. Types are defined using the JSON Schema specification (http://json-schema.org/).

Any type used by a stream must be registered before the stream can be created. Types can be created, updated, or deleted. Updating a type without updating the type's version will result in failure. Once a type is deleted, any operations on streams or objects using that type will fail.

The ``id`` keyword is required, and is used to associate a Stream, Span, Asset, or Link with a given data type.

The ``classification`` keyword must be set to one of ``stream``, ``asset``, ``link``, or ``span``, and is used to denote whether the type is to be used to define Streams, Assets, Links, or Spans. If omitted, the type is assumed to be used to define Streams.

An optional version keyword allows for multiple versions of the same type. If the version keyword is omitted, the version is assumed to be 1.0.0.0. Once a type has been defined, the type’s ``id`` cannot be reused unless a new version is specified.

One property must be designated as the index by supplying the ``index`` keyword with a value of ``true``. The designated index property is used to uniquely identify discrete Events, Spans, Assets and Links so that they can be updated or deleted after their initial creation.

When declaring an Asset type, one property may be optionally designated as the name of an asset by supplying the ``name`` keyword with a value of ``true``. If no property is declared to be the ``name``, the property marked as the ``index`` will be used as the name. Because the ``index`` must be unique across all assets, the ``name`` keyword allows for multiple distinct assets to share a common name.

Depending on the type's classification, additional properties are required:

=================== =============================
Type Classification       Required Properties
=================== =============================
Span                * ``StartTime``           
                    * ``EndTime``
Link                * ``Source``
                    * ``Target0`` ... ``TargetN``
=================== =============================

.. toctree::

   Type_Msg_Sample
