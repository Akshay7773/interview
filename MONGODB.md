## Q.1 Explain mongodb and its features.
MongoDB is an open-source document-oriented database that is designed to store a large scale of data and also allows you to work with that data very efficiently. It is categorized under the NoSQL (Not only SQL) database because the storage and retrieval of data in the MongoDB are not in the form of tables. 
Features of MongoDB –
 
*Schema-less Database*: It is the great feature provided by the MongoDB. A Schema-less database means one collection can hold different types of documents in it. Or in other words, in the MongoDB database, a single collection can hold multiple documents and these documents may consist of the different numbers of fields, content, and size. It is not necessary that the one document is similar to another document like in the relational databases. Due to this cool feature, MongoDB provides great flexibility to databases.
<br> 
*Document Oriented*: In MongoDB, all the data stored in the documents instead of tables like in RDBMS. In these documents, the data is stored in fields(key-value pair) instead of rows and columns which make the data much more flexible in comparison to RDBMS. And each document contains its unique object id.
<br> 

*Indexing*: In MongoDB database, every field in the documents is indexed with primary and secondary indices this makes easier and takes less time to get or search data from the pool of the data. If the data is not indexed, then database search each document with the specified query which takes lots of time and not so efficient.

*Scalability*: MongoDB provides horizontal scalability with the help of sharding. Sharding means to distribute data on multiple servers, here a large amount of data is partitioned into data chunks using the shard key, and these data chunks are evenly distributed across shards that reside across many physical servers. It will also add new machines to a running database.

*Replication*: MongoDB provides high availability and redundancy with the help of replication, it creates multiple copies of the data and sends these copies to a different server so that if one server fails, then the data is retrieved from another server.

*Aggregation*: It allows to perform operations on the grouped data and get a single result or computed result. It is similar to the SQL GROUPBY clause. It provides three different aggregations i.e, aggregation pipeline, map-reduce function, and single-purpose aggregation methods

*High Performance*: The performance of MongoDB is very high and data persistence as compared to another database due to its features like scalability, indexing, replication, etc.

<br> 

## Q.2 How does Mongodb stores data ? 
MongoDB stores data in a binary-encoded format called BSON (Binary JSON), which extends the JSON (JavaScript Object Notation) format to include additional types like Date and Binary. BSON is designed to be lightweight, traversable, and efficient for storage and retrieval of data.

Internally, MongoDB organizes data into collections, which are analogous to tables in relational databases, and documents, which are JSON-like data structures. Each document contains key-value pairs where keys are strings and values can be various data types supported by BSON. Documents within a collection do not need to have the same structure, allowing for flexible schema design.

Data is stored in MongoDB in a binary format on disk, organized into collections within databases. MongoDB uses a storage engine to manage data storage and retrieval. There are several storage engines available for MongoDB, including WiredTiger (the default as of MongoDB 3.2) and the in-memory storage engine.

WiredTiger, for example, organizes data into collections of BSON documents and uses compression and other techniques to optimize storage and performance. It also supports features like document-level concurrency control and checkpoints for durability.

Overall, MongoDB's storage architecture is designed to provide flexibility, scalability, and performance for a wide range of use cases, from small-scale applications to large distributed systems.


<br> 

## Q.3 Mongodb is Schema-less database. If yes, How do you create schema in mongodb ? 
As a NoSQL database, MongoDB is considered schemaless because it does not require a rigid, pre-defined schema like a relational database. The database management system (DBMS) enforces a partial schema as data is written, explicitly listing collections and indexes.

<br> 

## Q.4 Difference betweeen mongodb and mysql? 
Here's a brief comparison between MongoDB and MySQL in table format:

| Aspect         | MongoDB                                       | MySQL                                      |
|----------------|-----------------------------------------------|--------------------------------------------|
| Data Model     | Document-oriented (NoSQL)                    | Relational (SQL)                           |
| Schema         | Dynamic schema; no predefined schema required| Static schema; predefined schema required  |
| Query Language | MongoDB Query Language (MQL)                 | Structured Query Language (SQL)            |
| Scalability    | Horizontally scalable; sharding supported    | Vertically scalable; sharding possible     |
| Transactions   | Multi-document transactions available         | ACID-compliant transactions supported      |
| Data Integrity | Flexible; supports schema-less design        | Strict; enforces schema integrity          |
| Joins          | No support for joins; data denormalization   | Supports joins between related tables      |
| Indexes        | Supports various types of indexes             | Supports indexes for optimization          |
| Speed          | Generally faster for read-heavy workloads    | Generally faster for write-heavy workloads |
| Use Cases      | Big Data, real-time analytics, flexible data models | Traditional web applications, structured data |
| Examples       | Social media analytics, IoT, content management | E-commerce, banking, inventory management |

This table provides a simplified overview of some key differences between MongoDB and MySQL, but keep in mind that the choice between them depends on specific use cases, requirements, and preferences.
<br> 


## Q.5 What are the different data models in mongodb ?
Data in MongoDB has a flexible schema.documents in the same collection. They do not need to have the same set of fields or structure Common fields in a collection’s documents may hold different types of data.
Data Model Design
MongoDB provides two types of data models: — Embedded data model and Normalized data model. Based on the requirement, you can use either of the models while preparing your document.

### 1. Embedded Data Model
In this model, you can have (embed) all the related data in a single document, it is also known as de-normalized data model.

For example, assume we are getting the details of employees in three different documents namely, Personal_details, Contact and, Address, you can embed all the three documents in a single one as shown below −

```json
{
	_id: ,
	Emp_ID: "10025AE336"
	Personal_details:{
		First_Name: "Radhika",
		Last_Name: "Sharma",
		Date_Of_Birth: "1995-09-26"
	},
	Contact: {
		e-mail: "radhika_sharma.123@gmail.com",
		phone: "9848022338"
	},
	Address: {
		city: "Hyderabad",
		Area: "Madapur",
		State: "Telangana"
	}
}


```

### 2. Normalized Data Model
In this model, you can refer the sub documents in the original document, using references. For example, you can re-write the above document in the normalized model as:

Employee:
```json
{
	_id: <ObjectId101>,
	Emp_ID: "10025AE336"
}
Personal_details:

{
	_id: <ObjectId102>,
	empDocID: " ObjectId101",
	First_Name: "Radhika",
	Last_Name: "Sharma",
	Date_Of_Birth: "1995-09-26"
}
Contact:

{
	_id: <ObjectId103>,
	empDocID: " ObjectId101",
	e-mail: "radhika_sharma.123@gmail.com",
	phone: "9848022338"
}
Address:

{
	_id: <ObjectId104>,
	empDocID: " ObjectId101",
	city: "Hyderabad",
	Area: "Madapur",
	State: "Telangana"
}

```

<br> 



## Q.6 How does indexing works in mongodb? 
MongoDB uses multikey indexes to index the content stored in arrays. If you index a field that holds an array value, MongoDB creates separate index entries for every element of the array. These multikey indexes allow queries to select documents that contain arrays by matching on element or elements of the arrays.
<br> 


## Q.7 What is mongodb REPLICATION and SHARDING ? 
Replication and sharding are two key features in MongoDB that address scalability, availability, and data distribution:

1. **Replication**:
   - Replication involves maintaining multiple copies of data across multiple servers to ensure high availability and data redundancy.
   - In MongoDB, replication is achieved through replica sets, which consist of multiple MongoDB instances (nodes) where each node contains a copy of the data.
   - One of the nodes in the replica set serves as the primary node, handling all write operations and forwarding data changes to secondary nodes asynchronously.
   - Secondary nodes replicate data from the primary node, providing read scalability and failover capabilities. If the primary node fails, one of the secondary nodes automatically becomes the new primary node, ensuring continuous availability.
   - Replication enhances fault tolerance, data durability, and read scalability in MongoDB deployments.

2. **Sharding**:
   - Sharding involves partitioning data across multiple servers (shards) to distribute data storage and processing workload horizontally.
   - In MongoDB, sharding is achieved by dividing data into chunks based on a shard key, which is a field or combination of fields chosen to distribute data evenly across shards.
   - Each shard is a separate MongoDB instance or replica set that stores a subset of the data. MongoDB's config servers keep track of the mapping between data chunks and shards.
   - By distributing data across multiple shards, MongoDB can handle large datasets and high throughput by parallelizing read and write operations across shards.
   - Sharding provides horizontal scalability and allows MongoDB to scale out to accommodate growing data volumes and workload demands.

In summary, replication ensures data redundancy and fault tolerance, while sharding enables horizontal scalability and efficient data distribution in MongoDB deployments. Together, replication and sharding allow MongoDB to support large-scale, high-performance applications with high availability and scalability.

<br> 


## Q.8 Explain horizontal and vertical scaling in mongodb.
What is Scaling in MongoDB?
Scaling refers to the process of adapting your database infrastructure to accommodate increased data volumes and user demands. Hence, it eventually deals with meeting the additional needs of storage, memory, networking, and processing.

Consider an online marketplace where the volume of users and transactions steadily rises over time. The business initially uses a single MongoDB server to house all of its data, including user profiles, product descriptions, and order information. The need for scalability emerges when they realize that a single server is no longer adequate to satisfy the performance and scalability needs as the user base and volume of data grow.

Horizontal Scaling Vs Vertical Scaling in MongoDB
MongoDB Scaling can be achieved through two primary approaches: horizontal scaling and vertical scaling. Each approach offers distinct advantages and considerations, and understanding the differences between them is crucial.

What is Horizontal Scaling in MongoDB?
Horizontal Scaling, also known as scaling out, involves adding more servers and distributing the data across them. By adding more servers to your MongoDB cluster, you can handle increased data volumes, transactional loads, and concurrent user requests. Each server in the cluster shares a portion of the data, allowing for parallel processing and improved scalability.

### 1. Horizontal Scaling in MongoDB

Due to the difficulties of distributing relevant data among nodes, this is challenging with relational databases. Since collections in non-relational databases are independent and not relationally tied (for example, queries do not need to "join" them across nodes) this is made simpler.

Sharding and replica sets are two methods for horizontally scaling MongoDB.

What is Vertical Scaling in MongoDB?
Vertical scaling, also known as scaling up, involves increasing the capacity of individual servers within your MongoDB deployment. This can be achieved by upgrading hardware resources such as CPU, RAM, storage, or network capabilities. With vertical scaling, you enhance the capacity of a single server to handle increased workloads.

### 2. Vertical Scaling in MongoDB

Although both relational and non-relational databases can scale, the amount of processing power and throughput they can handle will ultimately reach a limit. As costs scale exponentially, there are also higher expenses when moving up to high-performance systems.

Horizontal Vs Vertical Scaling in MongoDB: Comparison
When deciding between horizontal and vertical MongoDB scaling, it's essential to consider the specific characteristics and requirements of your application or business.


here is the difference between horizontal and vertical scaling in mongodb  : 

![image](https://github.com/Akshay7773/interview/assets/91298667/18242c2d-8e4f-4106-a3ce-cba5e36aa978)

<br> 


## Q.10 What are replica sets ? Explain primary and secondary replica sets .
Replica sets in MongoDB are a group of MongoDB servers that maintain identical copies of the same data. They provide high availability and fault tolerance by allowing automatic failover in case of a primary node failure. Here's how replica sets work and the roles of primary and secondary nodes:

1. **Primary Node**:
   - The primary node is the primary member of the replica set and is responsible for handling all write operations (inserts, updates, and deletes) as well as read operations if the "read preference" is set to "primary".
   - The primary node receives write operations from clients and replicates these operations to all secondary nodes asynchronously, ensuring that all nodes eventually have the same data.
   - Clients interact with the primary node for write operations, and the primary node ensures data consistency across the replica set by replicating changes to all secondary nodes.

2. **Secondary Nodes**:
   - Secondary nodes are replica set members that replicate data from the primary node and serve read operations (if the "read preference" is set to "secondary").
   - Secondary nodes replicate data asynchronously from the primary node, meaning there may be a slight delay (known as replication lag) between data being written to the primary node and being replicated to secondary nodes.
   - Secondary nodes can serve read operations to distribute the read workload and improve read scalability. However, they cannot handle write operations directly.
   - In the event of a primary node failure, one of the secondary nodes is automatically elected as the new primary node through an election process managed by the replica set's internal consensus protocol (based on a priority configuration, availability, and the most up-to-date data). This ensures continuous availability and automatic failover without manual intervention.

Overall, replica sets in MongoDB provide fault tolerance, high availability, and data redundancy by maintaining multiple copies of data across multiple nodes. The primary node handles write operations and coordinates data replication, while secondary nodes replicate data and serve read operations to distribute the workload and improve scalability. Automatic failover ensures that the replica set remains available even in the event of a primary node failure.


<br> 



## Q.11 what is the use of capped collection in mongodb ? 

Capped collections in MongoDB are fixed-size collections that have a limited storage space and maintain insertion order based on insertion time. They are useful for certain use cases where you need to store a fixed number of records or logs and want to ensure high-performance insertion and retrieval operations.

<br> 


## Q.12 How can you store images, videos and other large files( >16mb ) in mongodb ?
In MongoDB, storing large files such as images, videos, and other binary data (>16MB) can be achieved using MongoDB's GridFS (Grid File System) feature. GridFS is a specification for storing and retrieving large files in MongoDB, and it enables efficient storage and retrieval of files exceeding the BSON document size limit of 16MB. Here's how you can use GridFS to store large files in MongoDB:

1. **GridFS Structure**: GridFS stores files in two collections: `fs.files` and `fs.chunks`.

   - `fs.files`: Contains metadata about the files, such as filename, content type, and other user-defined properties.
   - `fs.chunks`: Contains binary data chunks of the files. Each chunk typically has a default size of 255KB (configurable), and files are divided into multiple chunks as needed.

2. **Uploading Files**: To upload a file to MongoDB using GridFS, you can use the GridFS API provided by the MongoDB drivers. The API allows you to stream the file's data and metadata into GridFS, which automatically divides the file into chunks and stores them in the database.

3. **Retrieving Files**: To retrieve a file from MongoDB GridFS, you can query the `fs.files` collection based on criteria such as filename or metadata properties. You can then stream the file's chunks from the `fs.chunks` collection and assemble them into the original file.

4. **Managing Files**: GridFS provides features for managing large files, including capabilities to delete files, update metadata, and efficiently stream file data.

Here's a brief example using MongoDB's Node.js driver to upload a file to GridFS:

```javascript
const { MongoClient, GridFSBucket } = require('mongodb');
const fs = require('fs');

// Connection URI
const uri = 'mongodb://localhost:27017';

// Create a new MongoClient
const client = new MongoClient(uri);

async function uploadFile(filePath, filename) {
  try {
    // Connect to MongoDB
    await client.connect();

    // Open a GridFSBucket
    const db = client.db('my_database');
    const bucket = new GridFSBucket(db);

    // Open a stream to the file
    const readStream = fs.createReadStream(filePath);

    // Upload the file to GridFS
    await bucket.uploadFromStream(filename, readStream);

    console.log('File uploaded successfully.');
  } finally {
    // Close the connection
    await client.close();
  }
}

// Example usage
uploadFile('/path/to/myfile.jpg', 'myfile.jpg');
```

This example uploads a file named `myfile.jpg` to GridFS. You can customize it to handle other file types, provide metadata, and retrieve files as needed.


<br> 


## Q.13 Explain aggregation in mongodb.
Aggregation in MongoDB refers to the process of processing, transforming, and summarizing data from a collection to produce aggregated results. MongoDB provides a powerful aggregation framework that allows you to perform complex data analysis and manipulation operations, similar to SQL's GROUP BY, JOIN, and aggregation functions.

Key components of MongoDB's aggregation framework include:

1. **Pipeline**: Aggregation operations in MongoDB are constructed using pipelines, which consist of stages. Each stage performs a specific operation on the input documents and passes the results to the next stage in the pipeline. Common stages include $match (filtering documents), $group (grouping documents by a specified key), $project (reshaping documents), $sort (sorting documents), and $lookup (performing a left outer join with another collection).

2. **Operators**: MongoDB provides a wide range of aggregation operators that you can use within aggregation pipeline stages to perform various transformations and computations on the input documents. Examples include arithmetic operators ($add, $subtract), array operators ($push, $unwind), set operators ($setUnion, $setIntersection), conditional operators ($cond, $ifNull), and many more.

3. **Aggregation Functions**: MongoDB's aggregation framework supports various aggregation functions, such as $sum, $avg, $min, $max, $count, $first, and $last, which allow you to calculate aggregate values based on grouped data.

4. **Result Output**: Aggregation pipelines can produce various types of results, including aggregated values, grouped documents, computed fields, and reshaped documents. You can output the results of an aggregation pipeline to a new collection, return them as a cursor, or use them in subsequent aggregation stages.

Here's a simple example of using aggregation in MongoDB to calculate the total sales amount for each product category:

```javascript
db.sales.aggregate([
  {
    $group: {
      _id: "$category",
      totalSales: { $sum: "$amount" }
    }
  },
  {
    $sort: { totalSales: -1 }
  }
])
```

In this example, the aggregation pipeline consists of two stages:

1. $group stage: Groups documents by the "category" field and calculates the total sales amount for each category using the $sum aggregation operator.
2. $sort stage: Sorts the grouped results in descending order based on the total sales amount.

Aggregation in MongoDB provides a flexible and powerful way to perform data analysis, aggregation, and transformation operations on large datasets efficiently. It allows you to extract valuable insights from your data and generate meaningful summaries for reporting and decision-making purposes.

<br> 


## Q.14 What is meant by _id fiels in Mongodb?
In MongoDB, the `_id` field is a special field that serves as the primary key for documents within a collection. Every document in a MongoDB collection must have a unique `_id` field, which acts as a unique identifier for that document. If an `_id` field is not explicitly provided when inserting a document, MongoDB will automatically generate a unique ObjectId for the `_id` field.

Key points about the `_id` field in MongoDB:

1. **Uniqueness**: Each document in a collection must have a unique `_id` value. This uniqueness constraint ensures that each document can be uniquely identified within the collection.

2. **Primary Key**: The `_id` field serves as the primary key for documents in MongoDB collections. It facilitates efficient retrieval, updates, and deletions of documents by providing a unique identifier for each document.

3. **Automatic Generation**: If an `_id` field is not explicitly provided when inserting a document, MongoDB will automatically generate a unique ObjectId for the `_id` field. ObjectId values are 12-byte hexadecimal values consisting of a timestamp, machine identifier, process identifier, and a random counter.

4. **Custom `_id` Values**: You can provide your own custom `_id` values when inserting documents into a collection. Custom `_id` values can be of any BSON data type, such as string, integer, or ObjectId, as long as they are unique within the collection.

5. **Indexing**: MongoDB automatically creates an index on the `_id` field for each collection to enforce uniqueness and facilitate efficient lookup operations. This index helps improve the performance of queries that involve searching for documents by `_id`.

Overall, the `_id` field plays a crucial role in MongoDB collections by uniquely identifying each document and serving as the primary key for efficient data retrieval and manipulation operations.

<br>


## Q.15 How does mongodb creates ObjectID field? 
MongoDB creates ObjectId values based on a combination of the following components:

1. **Timestamp**: The first 4 bytes of an ObjectId represent a timestamp, indicating the creation time of the ObjectId value in seconds since the Unix epoch (January 1, 1970). This timestamp ensures that ObjectId values are roughly sorted by creation time, allowing for efficient retrieval of documents based on their insertion order.

2. **Machine Identifier**: The next 3 bytes of an ObjectId represent the identifier of the machine (or system) on which the ObjectId was generated. This identifier ensures that ObjectId values are unique across different machines, helping to prevent collisions when generating ObjectId values concurrently on multiple servers.

3. **Process Identifier**: The following 2 bytes of an ObjectId represent a process identifier (PID), which uniquely identifies the process that generated the ObjectId value. This component ensures that ObjectId values are unique within the context of a single process, even if multiple processes are generating ObjectId values concurrently.

4. **Counter**: The final 3 bytes of an ObjectId represent a counter value, which is incremented for each ObjectId generated within the same second by the same process. This counter ensures that ObjectId values are unique within the context of a single process and timestamp, preventing collisions when generating ObjectId values rapidly.

By combining these components, MongoDB generates unique ObjectId values that are roughly sortable by creation time, globally unique across different machines, and unique within the context of a single process and timestamp. This makes ObjectId values suitable for use as primary keys or unique identifiers for documents in MongoDB collections.
<br> 



## Q.17 Can you explain Map, Reduce process in MongoDB ? 
In MongoDB, the Map-Reduce process is a data processing paradigm used for performing aggregation and data analysis tasks on large datasets. It involves two main stages: the map stage and the reduce stage.

1. **Map Stage**:
   - In the map stage, a JavaScript function called the "mapper" is applied to each document in the input collection. The mapper function emits key-value pairs based on the content of the input documents.
   - The output of the map stage is a set of intermediate key-value pairs, where each key represents a grouping criterion and each value represents the data associated with that key.
   - The map function can extract and transform data from the input documents, perform filtering, or generate computed fields as needed.

2. **Reduce Stage**:
   - In the reduce stage, a JavaScript function called the "reducer" is applied to the intermediate key-value pairs produced by the map stage. The reducer function aggregates values for each unique key generated by the mapper function.
   - The reducer function combines values associated with the same key, typically by performing aggregation operations such as sum, count, average, or custom calculations.
   - The output of the reduce stage is a set of aggregated key-value pairs, where each key represents a unique grouping criterion and each value represents the result of the aggregation operation performed on the associated values.

3. **Finalize Stage (Optional)**:
   - In some cases, an optional finalize stage can be applied after the reduce stage. The finalize function can perform additional processing or transformations on the aggregated values before they are returned as the final output.
   - The finalize function is applied to each aggregated result produced by the reduce stage, allowing for further customization or refinement of the output.

4. **Output Stage**:
   - The final output of the Map-Reduce process is typically stored in a separate collection or returned as a result set, depending on the use case and requirements.
   - MongoDB provides options for specifying the output location and format of the Map-Reduce output, such as storing it in a new collection, merging it with an existing collection, or returning it as inline results.

Here's a basic example of using Map-Reduce in MongoDB to calculate the total sales amount for each product category:

```javascript
db.sales.mapReduce(
   function() {
      emit(this.category, this.amount);
   },
   function(key, values) {
      return Array.sum(values);
   },
   { 
     out: "total_sales_by_category"
   }
)
```

In this example, the map function emits key-value pairs where the key is the product category and the value is the sales amount. The reduce function sums up the sales amounts for each category, and the output is stored in a new collection named "total_sales_by_category".
<br>

## Q.18 What is the role of profiler in MongoDB ?
The database profiler collects detailed information about Database Commands executed against a running mongod instance. This includes CRUD operations as well as configuration and administration commands. The profiler writes all the data it collects to a system.
<br>


## Q.19 Can we use Regular Expressions in MongoDB ? 
Yes, MongoDB supports regular expressions (regex) in queries and various operations for pattern matching and string manipulation. You can use regular expressions in MongoDB for filtering documents, querying text fields, and performing string operations. Here are some common use cases for regular expressions in MongoDB:

1. **Querying Documents**: You can use regular expressions in queries to find documents where a field matches a specific pattern. MongoDB provides the `$regex` operator to perform regular expression matching.

   ```javascript
   // Find documents where the "name" field starts with "John"
   db.collection.find({ name: { $regex: /^John/ } })
   ```

2. **Text Search**: MongoDB's text search feature supports regular expressions for more advanced text search queries. You can use regular expressions to perform case-insensitive searches, partial matches, or more complex pattern matching.

   ```javascript
   // Perform a case-insensitive search for documents containing "example" in the "content" field
   db.collection.find({ content: { $regex: /example/i } })
   ```

3. **String Operations**: MongoDB's aggregation framework and update operations allow you to use regular expressions for string manipulation and transformation.

   ```javascript
   // Using regular expressions in aggregation to extract substrings
   db.collection.aggregate([
     {
       $project: {
         firstName: {
           $regexFind: {
             input: "$name",
             regex: /(\w+)/
           }
         }
       }
     }
   ])
   ```

4. **Indexing**: MongoDB supports indexing of fields for efficient regular expression queries. You can create regular expression indexes to improve the performance of regex queries on specific fields.

   ```javascript
   // Create an index on the "name" field for efficient regular expression queries
   db.collection.createIndex({ name: 1 }, { collation: { locale: "en", strength: 2 } })
   ```

Overall, regular expressions are a powerful feature in MongoDB that allow for flexible pattern matching and string manipulation operations, making it easier to query and analyze data in MongoDB collections.



## Q.20 How do you search for documents in which a specific field has one or more values ? 
To search for documents in MongoDB where a specific field has one or more values, you can use the `$exists` or `$ne` operators combined with the `$and` or `$or` operators. Here's how you can do it:

1. Using the `$exists` operator:
   
   If you want to find documents where a specific field exists and is not empty, you can use the `$exists` operator. This operator checks whether the specified field exists in the document.

   ```javascript
   // Find documents where the "field" exists and is not empty
   db.collection.find({ field: { $exists: true, $ne: null } })
   ```

2. Using the `$ne` operator:

   If you want to find documents where a specific field is not equal to a certain value (in this case, an empty value like an empty string ""), you can use the `$ne` operator.

   ```javascript
   // Find documents where the "field" is not equal to an empty value
   db.collection.find({ field: { $ne: "" } })
   ```

3. Combining with `$and` or `$or` operators:

   If you want to search for documents where a specific field has one or more values and potentially other conditions, you can combine the above queries with the `$and` or `$or` operators.

   ```javascript
   // Find documents where the "field" exists and is not empty, and optionally other conditions
   db.collection.find({
     $and: [
       { field: { $exists: true, $ne: null } },
       // Other conditions here (optional)
     ]
   })
   ```

   ```javascript
   // Find documents where the "field" is not equal to an empty value or other conditions
   db.collection.find({
     $or: [
       { field: { $ne: "" } },
       // Other conditions here (optional)
     ]
   })
   ```

These queries will retrieve documents where the specified field exists and has one or more values, excluding documents where the field does not exist or is empty. Adjust the query conditions as needed based on your specific requirements and the data structure of your MongoDB collection.


<br> 


## Q.21 Which commands are used to insert single and multiple documents into a collection ? 
To insert single and multiple documents into a MongoDB collection, you can use the `insertOne()` and `insertMany()` methods, respectively, in the MongoDB shell or any MongoDB driver. Here's how you can use these commands:

1. **Insert Single Document**:

   - `insertOne()`: This method inserts a single document into a collection. You provide the document to be inserted as an argument to the method.

   Syntax:
   ```javascript
   db.collection.insertOne(document)
   ```

   Example:
   ```javascript
   db.myCollection.insertOne({
     name: "John Doe",
     age: 30,
     email: "john@example.com"
   })
   ```

2. **Insert Multiple Documents**:

   - `insertMany()`: This method inserts multiple documents into a collection. You provide an array of documents to be inserted as an argument to the method.

   Syntax:
   ```javascript
   db.collection.insertMany([document1, document2, ...])
   ```

   Example:
   ```javascript
   db.myCollection.insertMany([
     { name: "Jane Smith", age: 25, email: "jane@example.com" },
     { name: "Mike Johnson", age: 35, email: "mike@example.com" },
     { name: "Emily Brown", age: 28, email: "emily@example.com" }
   ])
   ```

These commands will insert the specified documents into the `myCollection` collection in the current database. Make sure to replace `myCollection` with the name of your collection and adjust the document structure and field values as needed.

<br> 


## Q.22 What is the difference between $all and $in operator in mongodb ? 
In MongoDB, both the `$all` and `$in` operators are used to query arrays based on the presence of multiple values. However, they differ in their behavior and usage:

1. **$all Operator**:

   - The `$all` operator is used to select documents where the specified field contains an array that contains all of the specified values.
   
   - Syntax: `{ field: { $all: [value1, value2, ...] } }`
   
   - Example: Find documents where the "tags" field contains all of the specified tags ("mongodb", "database", and "nosql"):
     ```javascript
     db.collection.find({ tags: { $all: ["mongodb", "database", "nosql"] } })
     ```
   
   - The `$all` operator ensures that the field contains all the specified values in the query array. It does not require the array to contain only those values; it can contain additional elements.

2. **$in Operator**:

   - The `$in` operator is used to select documents where the specified field contains at least one of the specified values.
   
   - Syntax: `{ field: { $in: [value1, value2, ...] } }`
   
   - Example: Find documents where the "status" field contains either "active" or "inactive":
     ```javascript
     db.collection.find({ status: { $in: ["active", "inactive"] } })
     ```
   
   - The `$in` operator checks if the field contains any of the specified values in the query array. It does not require all the values to be present in the field.

In summary, the main difference between the `$all` and `$in` operators lies in their behavior regarding the presence of multiple values in an array field. `$all` requires all specified values to be present in the field, while `$in` requires at least one of the specified values to be present.

<br> 

## Q.23 What is shard key and mention the components of mongodb shareded cluster ? 
In MongoDB, a shard key is a field or combination of fields that determines the distribution of data across shards in a sharded cluster. The shard key is specified when creating a sharded collection and plays a crucial role in determining how data is distributed and queried in a sharded environment.

Key characteristics of a shard key include:

1. Uniqueness: The shard key should have sufficient cardinality to distribute data evenly across shards. Unique shard key values help prevent hot spots and ensure balanced data distribution.

2. Query Isolation: The shard key should be carefully chosen based on the application's query patterns to maximize query isolation. Queries that target a specific range of shard key values can be routed to a single shard for optimal performance.
   
3. Write Scaling: The shard key should support write scaling by distributing write operations across shards. A well-chosen shard key can distribute write operations evenly, preventing bottlenecks and ensuring efficient write throughput.

<br> 


## Q.24 The join clause is a key feature of relational database system . What is the mongodb equivalent if any and are there any limitations ? 
In MongoDB, the equivalent of a SQL join operation is achieved using the `$lookup` aggregation stage. The `$lookup` stage performs a left outer join between documents from two collections in the same database, based on matching criteria specified in the query.

Here's how you can use the `$lookup` stage to perform a join operation in MongoDB:

```javascript
db.collection.aggregate([
  {
    $lookup: {
      from: "foreignCollection",
      localField: "localField",
      foreignField: "foreignField",
      as: "joinedData"
    }
  }
])
```

- `from`: Specifies the name of the foreign collection to join with.
- `localField`: Specifies the field from the input documents (in the "collection" collection) to use for matching.
- `foreignField`: Specifies the field from the foreign documents (in the "foreignCollection" collection) to use for matching.
- `as`: Specifies the name of the output array field that will contain the joined documents.

This aggregation stage allows you to combine data from multiple collections into a single result set, similar to a SQL join operation.

Limitations of the `$lookup` stage in MongoDB include:

1. **Performance**: `$lookup` operations can be resource-intensive, especially when joining large collections or when there are no suitable indexes to support the join operation. Proper indexing and query optimization are crucial for efficient performance.

2. **Sharded Collections**: `$lookup` operations have limitations when performed on sharded collections across different shards. While `$lookup` is supported on sharded collections within the same shard, cross-shard joins are not directly supported and may require alternative approaches or denormalization.

3. **Pipeline Limitations**: The `$lookup` stage is part of the aggregation pipeline and has certain limitations compared to SQL joins, such as the inability to perform complex join conditions or joins across multiple levels of nesting. You may need to preprocess or reshape data before performing the join operation.

Despite these limitations, the `$lookup` aggregation stage in MongoDB provides a powerful mechanism for performing join operations between collections, enabling flexible data modeling and analysis in MongoDB databases.

<br> 

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
