---
uid: whatsNew
---

# What\'s New


Version 1.2 introduces the following incremental changes from version 1.1:

## Enhancements for Type messages:

- Ability to support type resuse using `reftypeid` defined on a [Property](xref:typePropertiesAndFormats) within a Type message.
- Addition of the `enum` keyword defined on a [Type Message](xref:typeMessages), used to create a reusable set of allowed values, and reference it as the datatype for a [Property](xref:typePropertiesAndFormats) using `reftypeid`.
- Support for `extrapolation` mode on the type, used to categorize the behavior of data being stored in instances.
- Ability to designate a property as holding data quality using `isquality` defined on a [Property](xref:typePropertiesAndFormats).
- Support for `minimum` and `maximum` type qualifiers defined on a [Property](xref:typePropertiesAndFormats).
- Support for `interpolation` mode defined on a [Property](xref:typePropertiesAndFormats), used to categorize the behavior of data being stored in properties.
- Simplified type delete messages requiring only `typeid`

## Enhancements for Container messages:

- Ability to override values of `properties` defined by a dynamic Type using the `propertyoverrides` keyword in the [Container Message](xref:containerMessages). Currently supported property overrides include `name`, `description`, `uom`, `minimum`, `maximum`, and `interpolation`.
- Ability to set the source of a stream of data using the `datasource` keyword defined on a [Container Message](xref:containerMessages).
- Support for `extrapolation` mode on the container, used to categorize the behavior of data being stored and override the type 'extrapolation' setting.
- Simplified container delete messages requiring `containerid` and `typeid`

## Enhancements for Data messages:

- Addition of the `property` keyword in the [__Link](xref:linkType) Data Message used to link Types and Instances of Types to a particular property.
- When linking to properties, the link can be defined by property to property, or defined by property to Type.
- Support for type-less static data values to be sent in a Data Message using the new keyword [properties](xref:dataMessages) within the Data Message.
- Simplified delete messages for static types which require only indexes

## Deprecated Features in OMF v1.2 specification:

- Specifying the version of a type when it is referenced is no longer supported. Types are considered immutable and can be referenced by their `typeid` alone.
- The `producertoken` field in the message header has been obsoleted, and is no longer supported.
