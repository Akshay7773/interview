
Absolutely! Here’s a **complete MongoDB script** with sample data and all the queries we discussed. You can copy-paste this directly into your MongoDB shell or Compass:

```javascript
// ------------------------
// 1. Insert Sample Data
// ------------------------
db.students.insertMany([
  {
    name: "Alice",
    age: 20,
    grade: "A",
    subjects: ["Math", "Physics"],
    enrolled: true,
    scores: { Math: 95, Physics: 88 }
  },
  {
    name: "Bob",
    age: 22,
    grade: "B",
    subjects: ["Biology", "Chemistry"],
    enrolled: true,
    scores: { Biology: 75, Chemistry: 80 }
  },
  {
    name: "Charlie",
    age: 21,
    grade: "C",
    subjects: ["Math", "Biology"],
    enrolled: false,
    scores: { Math: 65, Biology: 70 }
  },
  {
    name: "David",
    age: 23,
    grade: "A",
    subjects: ["Physics", "Chemistry"],
    enrolled: true,
    scores: { Physics: 90, Chemistry: 92 }
  },
  {
    name: "Eva",
    age: 20,
    grade: "B",
    subjects: ["Math", "Chemistry"],
    enrolled: false,
    scores: { Math: 85, Chemistry: 78 }
  }
]);

// ------------------------
// 2. Query Questions
// ------------------------

// a) Find students who are enrolled and have both "Math" and "Physics"
db.students.find({
  enrolled: true,
  subjects: { $all: ["Math", "Physics"] }
});

// b) Find students who have a Math score greater than 80
db.students.find({
  "scores.Math": { $gt: 80 }
});

// Optional: show only name and Math score
db.students.find(
  { "scores.Math": { $gt: 80 } },
  { name: 1, "scores.Math": 1, _id: 0 }
);

// c) Find students whose age is between 20 and 22 inclusive
db.students.find({
  age: { $gte: 20, $lte: 22 }
});

// Optional: show only name and age
db.students.find(
  { age: { $gte: 20, $lte: 22 } },
  { name: 1, age: 1, _id: 0 }
);

// d) Increase the age of all students by 1
db.students.updateMany(
  {},
  { $inc: { age: 1 } }
);

// Optional: check updated ages
db.students.find({}, { name: 1, age: 1, _id: 0 });

// e) Add "English" to the subjects of all enrolled students
db.students.updateMany(
  { enrolled: true },
  { $addToSet: { subjects: "English" } }  // use $push if duplicates are okay
);

// Optional: check updated subjects for enrolled students
db.students.find(
  { enrolled: true },
  { name: 1, subjects: 1, _id: 0 }
);

// f) Delete students who are not enrolled
db.students.deleteMany({ enrolled: false });

// Optional: check remaining students
db.students.find({}, { name: 1, enrolled: 1, _id: 0 });

// g) Delete students with grade "C"
db.students.deleteMany({ grade: "C" });

// Optional: check remaining students
db.students.find({}, { name: 1, grade: 1, _id: 0 });
```

---

Absolutely! The queries we’ve done so far cover the basics of **CRUD operations**. But in MongoDB, there are some **very useful query patterns** that are worth practicing, especially for real-world tasks. Here’s a list of important ones along with examples for your `students` collection:

---

### **1. Logical Operators**

* **$or** → match documents where **any** condition is true.

```javascript
// Students who are either enrolled or have grade "C"
db.students.find({
  $or: [
    { enrolled: true },
    { grade: "C" }
  ]
});
```

* **$and** → match documents where **all** conditions are true (optional, because multiple conditions in a query object are already ANDed)

```javascript
// Students who are enrolled AND age > 21
db.students.find({
  $and: [
    { enrolled: true },
    { age: { $gt: 21 } }
  ]
});
```

* **$not** → negates a condition

```javascript
// Students who do NOT have grade "A"
db.students.find({
  grade: { $not: { $eq: "A" } }
});
```

---

### **2. Sorting**

* Sort documents by a field ascending (`1`) or descending (`-1`)

```javascript
// Sort students by age ascending
db.students.find({}, { name: 1, age: 1, _id: 0 }).sort({ age: 1 });

// Sort students by grade descending
db.students.find({}, { name: 1, grade: 1, _id: 0 }).sort({ grade: -1 });
```

---

### **3. Limiting and Skipping**

* Useful for pagination

```javascript
// Get first 2 students sorted by age
db.students.find({}, { name: 1, age: 1, _id: 0 }).sort({ age: 1 }).limit(2);

// Skip the first 2 students
db.students.find({}, { name: 1, age: 1, _id: 0 }).sort({ age: 1 }).skip(2);
```

---

### **4. Count Documents**

* Count matching documents

```javascript
// Number of enrolled students
db.students.countDocuments({ enrolled: true });
```

---

### **5. Using $exists**

* Check if a field exists

```javascript
// Students who have a 'scores' field
db.students.find({ scores: { $exists: true } });
```

---

### **6. Using $in / $nin**

* Match documents where a value is in a list

```javascript
// Students with grade A or B
db.students.find({ grade: { $in: ["A", "B"] } });

// Students whose grade is NOT A or B
db.students.find({ grade: { $nin: ["A", "B"] } });
```

---

### **7. Aggregation (optional but very important)**

* Aggregation allows grouping, summing, averaging, etc.

```javascript
// Average Math score of all students
db.students.aggregate([
  { $group: { _id: null, avgMath: { $avg: "$scores.Math" } } }
]);

// Count of students per grade
db.students.aggregate([
  { $group: { _id: "$grade", count: { $sum: 1 } } }
]);
```

---

Absolutely! MongoDB interviews often focus not just on CRUD operations, but on **practical, real-world query patterns**, indexing, aggregation, and performance-related queries. Here’s a categorized list of **important MongoDB queries and operations that are commonly asked in interviews**:

---

## **1. Array Queries**

* **Find documents with a field containing a specific element**

```javascript
// Students taking Math
db.students.find({ subjects: "Math" });
```

* **Find documents containing all elements**

```javascript
// Students taking both Math and Physics
db.students.find({ subjects: { $all: ["Math", "Physics"] } });
```

* **Check array length**

```javascript
// Students taking exactly 2 subjects
db.students.find({ subjects: { $size: 2 } });
```

* **Find array elements greater than a value**

```javascript
// Students with any score in Math > 80
db.students.find({ "scores.Math": { $gt: 80 } });
```

---

## **2. Embedded Document Queries**

* **Query nested fields**

```javascript
// Students with Chemistry score > 80
db.students.find({ "scores.Chemistry": { $gt: 80 } });
```

* **Update nested fields**

```javascript
// Increase Math score by 5 for all students
db.students.updateMany({}, { $inc: { "scores.Math": 5 } });
```

---

## **3. Logical Operators**

* `$or`, `$and`, `$not`, `$nor`

```javascript
// Students either enrolled or grade C
db.students.find({ $or: [{ enrolled: true }, { grade: "C" }] });

// Students who are NOT enrolled
db.students.find({ enrolled: { $not: { $eq: true } } });
```

---

## **4. Comparison Operators**

* `$gt`, `$gte`, `$lt`, `$lte`, `$eq`, `$ne`

```javascript
// Students aged between 20 and 22
db.students.find({ age: { $gte: 20, $lte: 22 } });

// Students not having grade A
db.students.find({ grade: { $ne: "A" } });
```

---

## **5. Field Existence & Type**

* `$exists` → check if a field exists

```javascript
// Students with a 'scores' field
db.students.find({ scores: { $exists: true } });
```

* `$type` → check data type

```javascript
// Fields where age is a number
db.students.find({ age: { $type: "int" } });
```

---

## **6. `$in` and `$nin`**

```javascript
// Students with grade A or B
db.students.find({ grade: { $in: ["A", "B"] } });

// Students not having grade A or B
db.students.find({ grade: { $nin: ["A", "B"] } });
```

---

## **7. Sorting, Limiting, and Skipping**

```javascript
// Top 3 students by Math score
db.students.find({}, { name: 1, "scores.Math": 1, _id: 0 })
           .sort({ "scores.Math": -1 })
           .limit(3);

// Skip first 2 students sorted by age
db.students.find({}, { name: 1, age: 1, _id: 0 }).sort({ age: 1 }).skip(2);
```

---

## **8. Aggregation Framework (very important for interviews)**

* **Group, Sum, Avg, Max, Min**

```javascript
// Average Math score
db.students.aggregate([
  { $group: { _id: null, avgMath: { $avg: "$scores.Math" } } }
]);

// Count students per grade
db.students.aggregate([
  { $group: { _id: "$grade", count: { $sum: 1 } } }
]);
```

* **Filter and then aggregate**

```javascript
// Average Math score for enrolled students
db.students.aggregate([
  { $match: { enrolled: true } },
  { $group: { _id: null, avgMath: { $avg: "$scores.Math" } } }
]);
```

* **Project fields**

```javascript
// Show student name and total score
db.students.aggregate([
  { $project: { name: 1, totalScore: { $sum: ["$scores.Math", "$scores.Physics", "$scores.Chemistry", "$scores.Biology"] }, _id: 0 } }
]);
```

---

## **9. Text Search & Regex**

* **Regex queries**

```javascript
// Students whose name starts with 'A'
db.students.find({ name: { $regex: /^A/ } });
```

* **Case-insensitive search**

```javascript
db.students.find({ name: { $regex: /^alice$/i } });
```

---

## **10. Updates**

* `$inc`, `$set`, `$push`, `$addToSet`, `$pull`

```javascript
// Increment age by 1
db.students.updateMany({}, { $inc: { age: 1 } });

// Add "English" to subjects only if not present
db.students.updateMany({ enrolled: true }, { $addToSet: { subjects: "English" } });

// Remove "Biology" from subjects
db.students.updateMany({}, { $pull: { subjects: "Biology" } });
```

---

## **11. Deletes**

```javascript
// Delete students who are not enrolled
db.students.deleteMany({ enrolled: false });

// Delete students with grade C
db.students.deleteMany({ grade: "C" });
```

---

### **12. Indexing & Performance (discussion questions in interviews)**

* **Create index on a field**

```javascript
db.students.createIndex({ age: 1 });
db.students.createIndex({ "scores.Math": -1 });
```

* **Check indexes**

```javascript
db.students.getIndexes();
```

* **Explain query plan**

```javascript
db.students.find({ age: { $gte: 20 } }).explain("executionStats");
```

---

💡 **Tips for MongoDB interviews:**

* Be comfortable with **arrays, embedded documents, and aggregation**.
* Know the difference between `$push` and `$addToSet`.
* Understand **indexing** and how it affects query performance.
* Practice **sorting, limiting, skipping**, and **logical operators**.
* Be ready to write **real-world aggregation pipelines** (group, sum, average, project).

---

If you want, I can create a **single comprehensive MongoDB script** that includes **all these queries with examples for your `students` collection**, so you can just copy-paste and run it for practice.

Do you want me to do that?



=============> ACCUMULATORS <=========================
                1. $sum             2. $avg
                3. $max             4. $min


NOTE : MOST OF THE ACCUMULATORS ARE USED WITH GROUP

==========================> SUM <=========================================
1. $sum : 
     e.g.
        1.  {total: {$sum:"$quantity"}}         => it will sum the quantities 
        2.  {total:{$sum:1}}                   ==> it will add 1 everytime 


    examples :
```jsx
        db.persons.aggregate([
            {
                $group:{
                    _id:"$age",
                    count:{ $sum:1 }
                }
            }
        ])


        OUTPUT : 
            { _id:23, count:4.0 }
            { _id:28, count:9.0 }
            { _id:27, count:1.0 }
            { _id:31, count:7.0 }
```







====================IMPORTAANT ============================
I have two collection collection class and collection student

in class collection I have fields 
sr no    class    class_teacher 

and in student I have fields 
sr no     name contact  class

I want output in mongodb as 
sr no  name contact class class_teacher 

how can I write query for it  


```jsx
db.order_logs.aggregate([
  {
    $lookup:{
      from:"userds",
      localField:"borough",
      foreignField:"borough",
      as:"first"
    }
  },
  {
    $unwind:"$first"
  },
  {
    $project:{
      product:1,
      qty:1,
      borough:1,
      cuisine:"$first.cuisine",
      name:"$first.name"
    }
  }
  ])



```

===================> SUM , UNWIND AND GROUP <====================

  EXAMPLES =>

  ```jsx
    db.persons.aggregate([
        {unwind:"$tags"},
        {
            $group:{
              _id:"$tags"
              count:{$sum:NumberInt(1)}
            }
        }
    ])
```

  NOTE : 
        1.it will display all unique values inside array of tags and also count duplicates and displayed it 
        2. NumberInt() used for convert double values to integer values as $sum returns double values .




===============================================================================================================================

==========================> AVG <=========================================
2. $avg : 
    example:     
    
    ```jsx
        db.persons.aggregate([
    {
                $group:{
                    _id:"$eyeColor",
                    averageAge:{$avg:"$age"}
                }
            }
        ])
    ```
================================================================================================================================

SAME FOR MAX AND MIN  => 
    WE CAN GET VALUES OF MAX AND MIN IN A PERTICULAR GROUP.


================================================================================================================================


allowDiskUse : true
    1. All aggregation stages can use maximum 100 MB of RAM.
    2. Server will return error if RAM limit exceeded.
    3. Following option will enable MongoDB to write stages data to the temporal files .
        { allowDiskUse: true }



        e.g. 
            db.persons.aggregate([], { allowDiskUse:true })

================================================================================================================================


==========================> $count <============================]
    e.g.
        db.students.aggregate([{$count:"allDocumentsCount"},])

    it will return total number of documents present in students collection



    we will also get count using 
        db.students.find({}).count()

        this method also takes same time for returning count .




====================> GROUP AND COUNT <============================
```jsx
    db.student.aggregate([
        {$group:{_id:"$age"}},
        {$count:"age"}
    ])
```

    OUTPUT: count of distinct age
        i.e. age: 5


===========> MATCH , GROUP AND COUNT <===========================

```jsx
    db.student.aggregate([
        {$match:{age:{$gte:25}}},
        {$group:{_id:{eyeColor:"$eyeColor", age:"$age"}}},
        {$count:"eyecolorAndage"}
    ])
```



================================================================================================================================================


################################################ SORT ############################################################

NOTE : =>
    1 => it will sort data in ascending order 
   -1 => it will sort data in descending order .

   e.g. 
   ```jsx
        1. db.persons.aggregate([
              {$sort:{age: 1}}            SORT DATA IN ascending ORDER   
              OR
              {$sort: {age: -1}}          SORT DATA IN descending ORDER
          ])


        2. db.persons.aggregate([
            {$sort:{age:1, name:1}}
        ])
   ```

  in 2nd example it means that if if two fields have same age then it will sort on the basis of name , as like we can put multiple fields there.




===================> SORT WITH GROUP <=============================

 E.G. 
 ```jsx
        db.persons.aggregate([
            {$group:{_id:"$eyeColor"}}.
            {$sort:{_id:1}}
        ])
 ```


================================================================================================================================================
// aggregate returns everytime cursor

// FOR GETTING ALL DATA USING AGGREEGATION
db.collection_name.aggregate([]); //It will return all the data from perticular collection


// ----------------------->STAGE OPERATORS<------------------------------

1. $match       2. $group       3. $project 
4. $sort        5. $count       6. $limit
7. $skip        8. $out


1. $match : 
        e.g. 
           i.   db.students.aggregate([{$match:{city:"mumbai"}}])
           ii.  db.students.aggregate([{$match:{$age:{$gt:25}}}])
           iii. db.students.aggregate([{$match:{$and:[{$gender:"male"},{$age:{$gt:25}}]}}])


2. $group:
        it groups input documents by certain expressions . it returns distinct values 


        e.g. 
            i. db.students.aggregate([{$group:{_id:"$age"}}])
                 HERE OUTPUT IS : ==>
                        {
                                _id:"23"
                        }
                        {
                                _id:"54"
                        }

                that means it will return all unique values which are present in age of the students collection



           ii. Nested $group querry.

                db.students.aggregate([{$group:{_id:"$college.location.country"}}])

                it will return distinct countries 

        note: HERE _id IS MANDATORY FIELD. 




        WE CAN USE GROUP USING MULTIPLE FIELDS ALSO .

        E.G. 
                db.students.aggregate([{_id:{age:"$age", gender:"$gender"}}])

                OUTPUT: 
                        {"_id":{"age":34, "gender":"male"}}
                        {"_id":{"age":3, "gender":"female"}}
                        {"_id":{"age":32, "gender":"male"}}
                        {"_id":{"age":29, "gender":"female"}}
                        {"_id":{"age":34, "gender":"female"}}

                Note : IMPORTANT : =====> IT WILL NOT RETURN SAME OBJECT




=================================================================================================================================================


########################## COMBINE MATCH AND GROUP ##############################################

E.G. 
```jsx
        db.students.aggregate([
                {$match:{favFruit:"banana"}},
                {$group:{ _id :{age:"$age", eyeColor:"$eyeColor"}}}
        ])
```

   NOTE:   
          First it will check which students favorite fruit is banana and then it groups student on the basis of age and eyeColor



        if you want to return all data you must need to follow below rule : 
        ```jsx
         db.students.aggregate([
                 { $group: { _id: "$age", students: { "$first": "$$ROOT" } } },
                 { $project: { _id: 0, age: "$_id", student: "$students" } }
                ]);
        ```


NOTE : 
        if we swap both querries i.e . 
        
    ```jsx
        db.students.aggregate([
                {$group:{ _id :{age:"$age", eyeColor:"$eyeColor"}}},
                {$match:{favFruit:"banana"}}
        ])
    ```
  
   then there is no result, as DATA RETURNS FROM FIRST FIELD MUST BE IN _id FIELD. SO IT DOES NOT MATC FOR ANY favFruit field.

  
  
  
  =================FOR AVOIDING THIS DRAWBACK ==================
```jsx
db.students.aggregate([
                {$group:{ _id :{age:"$age", eyeColor:"$eyeColor"}}},
                {$match:{"_id.age":{$gt:30}}}
        ])

```
this query returns data of age is greater than 30



====================> OUT STAGE <=====================================
    1. $out must be last stage in the pipeline
    2. If output collection doesnt exist, it will be created automatically


example => 
```jsx
        db.persons.aggregate([
            {$group:{_id:"$age"}},
            {$out:"aggregationResults"}
        ])
```

  IMPORTANT NOTE:   
            1. It will not return anything but it will copy all the resultant data in new collection . 
            2. It will create new collection if it is now existed.
            3. In above example, aggregationResults is the new collection.
            4. It must be last stage of aggregation. i.e. after that we cant write any query or stages.


===========================================PROJECT AND LIMIT==========================================================================================

examples = > 
    1. {$project:{name:1, "company.title":1}}    => here both name and company title are displayed 
    2. {$project:{name:0, "company.title":1}}    => here name excluded and company.title included 
    3. {$project:{name:0, "company.title":0}}    => here both are excluded. and it will return other field by excluding these two field 
    4. {$project:{name:1,   newAge:"$age"}}      => here we give reference of age to newAge 


we can also give other names to the fields 

e.g. 
```jsx
    db.persons.aggregate([
        {$project:{
            _id:0,
            index:1,
            name:1, 
            info:{
                eyes:"$eyeColor",
                company:"$company.title",
                country:"$company.location.country"
            }
        }}
    ])
```


=======================================================================================================================================

############################################ LIMIT#######################################################

E.G.
```jsx
        db.persons.aggregate([
            {$limit:100},
            {$match:{$age:{gte:25}}}
        ])

```
   OUTPUT => it will first get first 1000 rows and then set query of match for that 100 rows .


=======================================================================================================================================

============> UNARY OPERATORS <=========================

        1. $type           2. $or
        3. $lt             4. $gt
        5. $and            6. $multiply


1. $type: 
    example =>
   ```jsx
        db.persons.aggregate([
            {
                $project:{
                    name:1,
                    ageType:{ $type: "$age" }
                }
            }
        ])
    ```



   ==================================================> UNWIND <=========================================================

if we want to apply group for array then or value inside that perticular array the n we need to use UNWIND 

UNWIND : 
    it split document with specified array to several documents, one document per array element. 


 e.g. 
    1. {$unwind:"$tags"}       // here tags is an array inside perticular collection 
```jsx
    db.persons.aggregate([
        {$unwind:"$tags"},
        {$project:{name:1, index:1, tags:1}}
    ])
```

  NOTE => 
        suppose if one of the document have 3 values in his tags array then it will create 3 different document for each of this value 




=================> GROUP WITH UNWIND < ===============================

NOTE : suppose IF WE WANT TO GROUP ELEMENT ON THE BASIS OF ARRAY VALUE THEN 

e.g.
```jsx
db.persons.aggregate([
    {$unwind:"$tags"},
    {$group:{_id:"$tags"}}
])
```
