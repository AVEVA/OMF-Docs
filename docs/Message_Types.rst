Message Types
=============
Messages sent to a PI system fall into four categories: Type messages, Object messages, Stream messages, and Data messages. Within each category, three types of actions can be specified: Create, Update, and Delete.

Each message can perform operations across multiple streams, types, or data objects by bulking each individual JSON object into a JSON array.

To achieve optimal throughput, bulking and compression of messages is recommended. 

.. toctree::

   Type_Messages
   Object_Messages
   Stream_Messages
   Data_Messages
