# MongoDB

## Getting Started

### Runing on terminal
 ```
 mongosh // opens mongodb shell on terminal
 ```

### Viewing Databases

```
show dbs
```
### Creating/Changing Database
Syntax: 
```
use database_name
```
Example

```
use school
```
### Adding collection to Database
```
db.createCollection('students')
```
### Droping Database

```
db.dropDatabase()
``` 

### Creating a document
#### Inserting only one document
Syntax:
```
db.collectionname.insertOne({name:value})
```
Example:
```
db.students.insertOne(
{
    name:"Hojo"
    , age:"20",
    gpa: 4
})
```

#### Inserting  many document

```
db.students.insertMany(
[{
    name:"Hojo",
    age:20,
    gpa:4
},
{
    name:"Anil",
    age:20,
    gpa:3.9
},
{
    name:"Bob",
    age:23,
    gpa:3.9
}])
```
### DataTypes

```
db.students.insertOne(
{   name:"gaurab khanal" // String
    ,age:19, // Integer
    gpa:4.0, // Float
    fullTime:false, // boolean
    registerDate: new Date(), // Date
    graduationDate:null, // null
    courses:["Physics","Calsulus","Chemistry"], // Array
    address:{stree:"123 Mountain",city:"Itahari", zip:1332} // Objects
})
```

### Returning all documents
Syntax:
```
db.collection_name.find()
```
Example:
```
db.students.find()
```

### Sorting Documents
####   Alphabetical order

```
db.students.find().sort({name:1})// 1 for ascending aplabetical order, -1 for vice versa // instead of name you can write according to which value you want to sort
```

#### Sort by GPA

```
db.students.find().sort({gpa:1})
```

### Limiting the return of Documents

```
db.students.find().limit(1)// 1 represents number of documents to be returned.
// Note: Here 1 is just a normal math, it doesnot act as array maths
```

### Combine Sort and Limit

Returning only 2 students with highest GPA

```
db.studends.find().sort({gpa:-1}).limit(2)
```

### Working with find method
Syntax:
```
db.students.find({query},{projection})
```
Exmaple:

```
db.students.find({gpa:4}) //in query there is gpa:4, means it will return all documents with gpa 4.
```
Note: query return documents with certain condition fulfilled like as above gpa should be 4.

projection return only value which is mentioned as true from all documents.
```
db.students.find({},{gpa:true})
db.students.find({},{gpa:true, name:true})
```

### Updating Document

#### Updating only one document
Syntax:
```
db.students.updateOne({filter}, {update})
```
Example:
```
db.students.updateOne({name:"Bob"},{$set:{fullTime:true}})
```
#### Updating many documents
```
db.students.updateMany({},{$set:{result:"Pass"}})
```

### Removing field from document

```
db.students.updateOne({name:"Bob"},{$unset:{fullTime:""}})
```

### Deleting Document
#### Deleting only one Document
```
db.students.deleteOne({name:"Bob"})
```

#### Deleting only Many Document

```
db.students.deleteMany({DOB:{$exists:false}})
```

### Comparasion Operator
- Not Equal to
```
db.students.find({name:{$ne:"Hojo"}}) // find everyname that isn't Hojo
// ne => not equals
```
- Less than
```
db.students.find({age:{$lt:20}}) // find age which is less than 20
```
- Less than equal to

```
db.students.find({age:{$lte:19}})
```
- Less than equals to and greater than equals to 

```
db.students.find({gpa:{$gte:3.8,$lte:4}})
```

- In operator (in)
```
db.students.find({name:{$in:["Bob","Hojo"]}})
// Return student document whose name is either Bob or Hojo
```
- Not In (nin)

```
db.students.find({name:{$nin:["Bob","Hojo"]}})
// Return every students document whose name isn't Hojo or Bob.
```

### logical Operators:

- $and

```
db.students.find({$and:[{result:"Pass"},{age:{$lte:20}}]})
```

- $or

```
db.students.find({$or:[{result:"Pass"},{age:{$lte:20}}]})
```
- $nor

```
db.students.find({$or:[{result:"Fail"},{age:{$lte:20}}]})
```

-  $not

```
db.students.find({gpa:{$not:{$gt:3.8}}})
```


