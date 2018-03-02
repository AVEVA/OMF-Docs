The OSIsoft Message Format 
==========================

v1.0
-----


Overview
--------

The OSIsoft Message Format (OMF) defines a set of message headers and message bodies that 
are used to generate compliant messages for inputting data into either an on-premises PI 
System, OSIsoft Cloud Services, or another compliant backend system.

OMF can be used to develop data acquisition applications on platforms and in languages 
for which there are no supported OSIsoft libraries.

The OMF specification does not define or depend on any particular binary message protocol 
(HTTP, AMQP, Kafka, and so on.) Rather, it is based on an abstract message type, where a 
message consists of a set of key / value pairs, called the header, and a binary 
payload, called the body. OMF messages can thus be constructed using any message 
protocol that defines headers and bodies. For up-to-date information about the specific 
binary protocols currently supported by OSIsoft systems, consult the Qi and PI 
Connector Relay documentation.

Contents
--------

.. toctree::

   Headers
   Message_Types
   Type_Messages
   Container_Messages
   Data_Messages
   
HTTP Behaviors
--------------

While the OMF specification does not define a particular binary message protocol, OSIsoft 
systems accepting OMF over HTTP conform to a set of behaviors described in this section.

.. toctree::
   
   Message_Size
   Standard_Responses

