Message Types
=============

OMF messages fall into three categories: Type, Group, and Data messages. Within each category, three types of actions can be specified: Create, Update, and Delete.

Each message can bulk individual JSON objects into a JSON array. Within a given array, all objects must be of the same message type: Type, Group, or Data. 

To achieve optimal throughput, bulking and compression of messages is recommended.

.. toctree::

   Type_Messages
   Group_Messages
   Data_Messages
