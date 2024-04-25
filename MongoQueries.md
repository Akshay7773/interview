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
