---
uid: index
---

Open Message Format
======================

# Overview

The Open Message Format (OMF) defines a set of message headers and bodies that can be used to generate messages for ingestion into a compliant back-end system.

OMF can be used to develop data acquisition applications on platforms and in languages for which there are no supported OSIsoft libraries.

OMF itself does not define or depend on any particular binary message protocol (HTTP, AMQP, Kafka, etc.) It is instead based on an abstract message type,
where a message consists of a set of key / value pairs, called the headers, and a binary payload, called the body. OMF messages can thus be constructed
using any message protocol that defines headers and bodies. For up to date information on the specific binary protocols currently supported by OSIsoft
systems, consult the AVEVA Data Hub, AVEVA Data Hub, PI Web API, and Edge Data Store documentation.

Please note that anything defined in this document, such as keywords and enumerated
values, is treated as case insensitive. Case sensitivity for all user specified values
is determined by the rules of the backend system.
