## Q.1 Explain mongodb and its features.
MongoDB is an open-source document-oriented database that is designed to store a large scale of data and also allows you to work with that data very efficiently. It is categorized under the NoSQL (Not only SQL) database because the storage and retrieval of data in the MongoDB are not in the form of tables. 
Features of MongoDB –
 
Schema-less Database: It is the great feature provided by the MongoDB. A Schema-less database means one collection can hold different types of documents in it. Or in other words, in the MongoDB database, a single collection can hold multiple documents and these documents may consist of the different numbers of fields, content, and size. It is not necessary that the one document is similar to another document like in the relational databases. Due to this cool feature, MongoDB provides great flexibility to databases.
Document Oriented: In MongoDB, all the data stored in the documents instead of tables like in RDBMS. In these documents, the data is stored in fields(key-value pair) instead of rows and columns which make the data much more flexible in comparison to RDBMS. And each document contains its unique object id.
Indexing: In MongoDB database, every field in the documents is indexed with primary and secondary indices this makes easier and takes less time to get or search data from the pool of the data. If the data is not indexed, then database search each document with the specified query which takes lots of time and not so efficient.
Scalability: MongoDB provides horizontal scalability with the help of sharding. Sharding means to distribute data on multiple servers, here a large amount of data is partitioned into data chunks using the shard key, and these data chunks are evenly distributed across shards that reside across many physical servers. It will also add new machines to a running database.
Replication: MongoDB provides high availability and redundancy with the help of replication, it creates multiple copies of the data and sends these copies to a different server so that if one server fails, then the data is retrieved from another server.
Aggregation: It allows to perform operations on the grouped data and get a single result or computed result. It is similar to the SQL GROUPBY clause. It provides three different aggregations i.e, aggregation pipeline, map-reduce function, and single-purpose aggregation methods
High Performance: The performance of MongoDB is very high and data persistence as compared to another database due to its features like scalability, indexing, replication, etc.
## Q.2 How does Mongodb stores data ? 

## Q.3 Mongodb is Schema-less database. If yes, How do you create schema in mongodb ? 

## Q.4 Difference betweeen mongodb and mysql? 

## Q.5 What are the different data models in mongodb ?

## Q.6 How does indexing works in mongodb? 

## Q.7 What is mongodb REPLICATION and SHARDING ? 

## Q.8 Explain horizontal and vertical scaling in mongodb.

## Q.9 When should we embed one document with another ? 

## Q.10 What are replica sets ? Explain primary and secondary replica sets .


## Q.11 what is the use of capped collection in mongodb ? 


## Q.12 How can you store images, videos and other large files( >16mb ) in mongodb ?

## Q.13 Explain aggregation in mongodb.


## Q.14 What is meant by _id fiels in Mongodb?

## Q.15 How does mongodb creates _id field? 

## Q.16 What are some utilities for Backup and restoring in MongoDB ? 

## Q.17 Can you explain Map, Reduce process in MongoDB ? 

## Q.18 What is the role of profiler in MongoDB ?

## Q.19 Can we use Regular Expressions in MongoDB ? 

## Q.20 How do you search for documents in which a specific field has one or more values ? 


## Q.21 Which commands are used to insert single and multiple documents into a collection ? 

## Q.22 What is the difference between $all and $in operator in mongodb ? 

## Q.23 What is shard key and mention the components of mongodb shareded cluster ? 

## Q.24 The join clause is a key feature of relational database system . What is the mongodb equivalent if any and are there any limitations ? 

## Q.25 What is lookup in mongodb ? 

## Q.26 Can we create own functions in mongodb ? 

## Q.27 Whats the difference between find and findOne in mongodb ? 

## Q.28 What is explain in mongodb? 

## Q.29 What are docuements in mongodb? 

## Q.30 Transactions in mongodb ? 

## Q.31 What is replica set in mongodb ? 

## Q.32 How to use text search in mongodb ? 

## Q.33 What is collection , document in mongodb ? 

## Q.34 What are the different types of indexing in mongodb ? 

## Q.35 What is MapReduce in mongodb ? 

## Q.36 What is GridFS in mongodb ? 

## Q.37 What is difference between primary and secondary key in mongodb ? 

## Q.38 How does mongodb handle transactions ? 

## Q.39 How does mongodb handle security ? 

## Q.40 What is difference between join and lookup in mongodb ? 


## Q.41 How does MongoDB handle data backup and recovery ? 

## Q.42 What is NameSpaces in mongodb ? 

## Q.43 Mention what is ObjectID composed of ? 

## Q.44 What is BSON in mongodb? 

## Q.45 What are the supported data types in mongodb ? 

## Q.46 What is the use of pretty method in mongodb ? 

## Q.47 Difference between insert(), insertOne(), insertMany() ? 

## Q.48 What is bulk write operation in mongodb ? 

## Q.49 What is the use of $set in mongodb ? 

## Q.50 Difference between update and findOneAndUpdate() 

## Q.51 Difference between drop and remove  ? 
  drop() function removes the specified collection from the database .
  remove() function deletes documents from a collection.

<br> 

## Q.52 Difference between createIndex and reIndex 
  createIndex : builds an index on a collection.
  reIndex : rebuilds all existing indexes on a collection .


<br> 

## Q.53 How to drop collection ? 

## Q.54 How to rename collection ? 

## Q.55 What is the difference between findModify() and findOneAndUpdate() ? 

## Q.56
