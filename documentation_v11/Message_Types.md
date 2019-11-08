---
uid: messageTypesv11
---

# Message Types

OMF messages fall into three categories: Type, Container, and Data messages. Within each category, three types of actions can be specified: Create, Update, and Delete.

Each message bulks individual JSON objects into a JSON array. Within a given array, all objects must be of the same message type: Type, Container, or Data.

To achieve optimal throughput, bulking and compression of messages is recommended.

