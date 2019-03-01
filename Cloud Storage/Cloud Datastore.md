# Google Cloud Datastore

https://cloud.google.com/datastore/

## What is Datastore?

 Instead of writing Data with relations into a Relational Database, we can write them as they are, as Objects directly into a Datastore. 



* Document orientient NoSQL storage.
* Scales up to Terabytes of Data

- Stores a Key Hashmap to an Object
- Key value structure
- Transactions are supported to read and write structured data
- It's like a persistent HashMap
- In Memory, Objects can be saved directly to the DataStore
  - Author sascha = new Author("Sascha Heyer"),
  - datastore.save().entity(sascha);
- Not used for OLTP or OLAP
- Query execution time depends of the size of the returned results (not size of data set)
  - Hash based indicies
  - Indicies are fast to read, slow to write
  - Therefore don not use Datastore for write intensive data