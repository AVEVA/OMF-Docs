Message Types
=============
Messages sent to a PI system fall into three categories: Stream messages, Type messages, and Data messages. Within each category, three types of actions can be specified: Create, Update, and Delete.

Each message can perform operations across multiple streams, types, or data objects by bulking each individual action into a single message.

To achieve optimal throughput, bulking and compression of messages is recommended. 

.. toctree::

   Type_Messages
   Stream_Messages
   Data_Messages