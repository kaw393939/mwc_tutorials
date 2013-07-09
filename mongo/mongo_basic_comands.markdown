MongoDB Basic Commands
MongoDB Terminology and Concepts 
Before starting with the MongoDB Basic Commands, you should know first by heart what each terminology that will be used in this tutorial means for you to understand what is going on with the examples.  
Database – It is a physical container for collections. Each database gets its own set of files on the 
	file system. A singled MongoDB server typically servers multiple databases. 

Collection – This is a grouping of BSON documents. Collections do not enforce a schema, but
 they are otherwise mostly analogous to RDBMS tables. 
 
Document – It is a record in a MongoDB collection, and the basic unit of data in MongoDB. 
	Documents are analogous to JSON objects, but exists in the database in a more type-rich 
	format known as BSON.  

Field – It is a name-value pair in a document. Documents have zero or more fields. 
Fields are analogous to columns in relational databases like Oracle and MySQL. 

Primary key – It is a record’s unique, immutable identifier. In a relational database system, the 
	primary key is typically an integer stored in each row/record’s id field. In MongoDB, the 
	_id field holds a document’s primary key which is usually a BSON ObjectId.

Index – It is a data structure that optimizes queries allowing you to locate documents based on 
	the values stored in certain specified fields. Fundamentally, indexes in MongoDB are 
	similar to indexes in other database system. 

Aggregate framework – It allows MongoDB to provide native aggregation capabilities that 
	corresponds to many common data aggregation functions and operations in SQL. 
In an RDBMS, this is analogous to aggregate functions and operations. 


Starting with MongoDB Shell
To get started with this tutorial, open a GNU terminal and start mongoDB with the mongo command. Remember, mongo command will start the mongoDB Shell Command Line where you can execute MongoDB commands. 
To check your databases, use the command: 

	$ show dbs 
This MongoDB command will list all databases in your MongoDB. You have to select from the list a database to use that you will perform data operations and manipulations. To select a database type this command with the following syntax: 

	$ use <database_name> 
	Ex: $ use test 
To know what currently database you are using, type this command below. It will return the name of the database you are using: 

	$ db 
You can also type the command below in the mongo shell to list the current collections in the database: 
$ show collections 
However, let’s say you want to create a new database and not use the existing ones in your MongoDB Shell, you can simple type the command below: 

	$ use <database_name> 
	Ex: $ use nba
Here in the example above, nba database is not yet created and does not have any collections or documents in it. You don’t need to worry using a database since it is not yet created, because MongoDB will automatically create it for your. After issuing the use database command, you can now start creating a collection which will be discussed later in this tutorial. 



Core MongoDB Operations (CRUD) 
CRUD stands for create, read, update, delete, which are four of the essential core database operations used in database driven application development. 
NOTE: For the following examples, we will use the nba database that we created earlier. You have to issue the command to use the nba database before proceeding and trying the examples below.
Create

The insert ( ) Operation
You can create documents in a MongoDB collection using insert and upsert operations.  Let’s look at how the insert( ) method works. The insert( ) is the primary method to insert a document or documents into a MongoDB collection. This method is analogous to the INSERT statement of SQL and has the following syntax: 

	$ db.collection.insert( <document> ) 
	Ex: $ db.players.insert( { _id: 1, 
    name: { first: “Kobe”, last: “Bryant” }, 
    team: “Los Angeles Lakers”, number: 8, 
    college: “Maryland College”
       	} )
In the example above, the command inserts a document into players collection with the fields specified in the nba database that we selected. Whenever the collection is not yet created, MongoDB automatically creates it for you just the same as creating a database before. However, if you already have fields in a certain collection, let’s say this players collection has fields named _id, name.first, name.last, number, college and team. If you will try to insert another document that will have all the fields mentioned, but with an additional field not yet created before, MongoDB will add it. 
	
	Ex: $ db.players.insert( { name: { first: “LeBron”, last: “James” }, 
     team: “Miami Heat”, position: “Small Forward”, 
     age: 28, years_pro: 8			 
      	 } ) 
In the example we have here, you are inserting a document with the previous fields named and including position,age and  years_pro fields that are new in this document. This is just fine because MongoDB will insert it for you without any trouble that it is not declared yet, though it will leave the other fields blank. Also, notice in this example that the _id field which acts as a primary key is not specified in the insert( ) method. MongoDB will automatically assigns a random BSON-type ObjectId as the default value for the _id field that is not specified. Also, take a look at the name field, this has a sub-fields which are called as subdocuments. The name field contains a subdocument that can be access by using the dot notation that will be discussed later.

Bulk Insert Multiple Documents
You can insert bulk documents into a collection by passing an array of documents to the insert ( ) method. To illustrate this operation, the following example inserts 3 documents into the players collection.

	$ db.players.insert ([ { name: { first: “Toni”, last: “Parker” }, team: “San Antonio Spurs” }, 
          { name: { first: “Chris”, last: “Paul” }, team: “Los Angeles Clippers” }, 
          { name: { first: “Carmelo”, last: “Anthony” } team: “New York Knicks” }])

Update ( ) Operations with the upsert Flag
The update ( ) operation in MongoDB accepts an “upsert flag that modifies the behavior of update ( ) method from updating existing documents, to inserting data. The update ( ) method with the upsert flag eliminates the need to perform an additional operation to check for existence of a record before performing either an update or an insert operation. These update operations have the use <query> argument to determine the write operation. Take note, if the query matches an existing document(s), the operation is an update ( ). However, if the query matches no document in the collection, the operation is an insert ( ). An upsert operation has the following syntax: 
> 
	$ db.collection.update( <query>, <update>, { upsert : true } )
	Ex: $ db.players.update( { name: { first: “Kobe”, last: “Bryant” } }, 
    { awards: [“Season 2011 MVP Award”, “4th Best All-time scorer”]}, 
    { upsert: true } )
In the example, you are inserting a document with the upsert operation flag set to true which will check first if the query matches an existing document, if there is, it will update the document. If there is no matches with the documents in the collection, it will insert this particular document.

Inserting a document with an array
You can also insert a field with an array for purposes of lists, collective data and other uses. In the example above, you just inserted a document with an array in the awards field. This is just a simple example showing how to insert an array in a field of a document in MongoDB.  

Insert a Document with save ( ) 
The save ( ) method performs an insert if the document to save does not contain the _id field. In this following example, the save ( ) operation does an insert into the players collection since the document does not contain the _id field: 
$ db.players.save( { name: { first: “Derrick”, last: “Rose” }, team : “Chicago Bulls” } )

Inserting a Document that Contains field and value pairs 
If no document matches the <query> argument, the upsert method performs an insert. If the <update> argument includes only field and value pairs, the new document contains the fields and values specified in the <update> argument. If the <query> argument does not include an _id field, the operation adds the _id field and generates a unique ObjectId for its value. Take a look at our next example in which inserts a new document into the players collection: 
> 
	$ db.players.update( { name: { first: “Chris”, last: “Paul” } }, 
          { name: { first: “Chris”, last: “Paul”}, team: “Los Angeles Clippers”, 
             age: 25, birthdate: new Date(‘Sep 28, 1988’), 
	conference: “Western” }, 
          { upsert : true } )




Read
The find ( ) operation
You can read or retrieve documents in MongoDB from a collection. In the mongo shell, the
find( ) method perform read operations. Using the find( ) method in the following syntax: 

	$ db.collection.find( <query> ,  <projection> )  
Take a look at the arguments above. The <query> argument of the find( ) method holds this query document. A read operation without a query document will return all documents in the collection. The <projection> argument describes the result set in the form of a document. Projections specify or limit the fields to return. Without a projection, the operation will return all fields of the documents. It will be better to specify a projection if your documents are larger, or when your application only needs a subset of the available fields. The order of the documents returned by a query is not defined and is not necessary consistent unless you specify a sort using the sort( ) method. This operation is somewhat similar to what the SELECT statement in SQL does in relational databases. 
Typing any of the commands below in the mongo shell will select all documents in the collection. These two commands produces exactly similar results. 

	$ db.players.find( { } )  
	$ db.players.find ( )
You can also use this command below to retrieve documents in a well-presented way as it does print on your mongo shell the document contents with indentations and spacing: 

	$ db.players.find( ).pretty ( ) 

Equality Matches
For an example, the following operation on the players collection selects documents where the team field is 
exactly Miami Heat. 

	$ db.players.find( { team : “Miami Heat” } )



Subdocuments
When the field holds an embedded document (i.e. subdocument), you can either specify the entire subdocument as the value of a field, or “reach into” the subdocument using the dot notation, to specify values for individual fields in the subdocument. Equality matches within subdocuments select documents if the subdocument matches exactly the specified subdocument, including the field order. Let’s have an example below to clear this concept: 

	$ db.players.find( { 
	name: { 
	first: “LeBron”, last: “James” 
	}
      } )
This query is an equality match for specific fields within subdocuments select documents when the field in the subdocument contains a  field that matches the specified value. You can also do the query above through the following example in which the query uses the dot notation to match all documents where the value of the field name is a subdocument that contains field first with the value ‘LeBron’ and may contain other fields: 

	$ db.players.find( { ‘name.first’ : ‘LeBron’} )

Working with Arrays 
Query an Element
The following operation returns a cursor to all documents in the players collection where the array field awards contains the element ‘MVP’: 

	$ db.players.find({ awards: ‘MVP’ } )




 
Logical Operators 
OR Disjunctions 
The following operation returns a cursor to all documents in the players collection where either the field first in the sub-document name starts with the letter L or where the age is less than 30: 

	$ db.players.find({
     $or: [ 
	{ “name.first” : /^L/ },
	 { age : { $lt: 30 } } ]
    	})
AND Conjunctions 
The following operation returns a cursor to all documents in the players collection where the field first in the subdocument names starts with the the letter D and where the team field contains the word Miami: 

	$ db.players.find({ “name.first” : /^D/, “team” : /^Miami/ })

Specifying Fields to Return
In the example above, it will return all of my contact persons from the players collection as documents that has Miami Heat matching with the field team. In this case, we haven’t set a projection yet, this is all a simple query. But in the next example here, it will show you how a projection is used. 

	$ db.players.find( { team : “Miami Heat” , { name : 1, address : 1, age : 1 }  })
In this example above, the projection limits the fields of the documents that will be returned from the players collection corresponding to the query. 
On Arrays and Subdocuments

	$ db.players.find( { }, { _id: 0, “name.last” : 1, awards: { $slice : 2 } } )
In this example above, you are specifying the query to return the name.last and awards field, but limit the elements of the awards field array only to 2 elements. This example also explicitly excludes the _id field from the query to be returned. 

Return All but the Excluded Fields 
If you want to return all the fields in a document(s) in a collection, you can specify it. In this following example, the operation finds all documents in the players collection that contains the element Miami Heat and returns all fields except the _id field, the first field in the name subdocument, and the conference field from the matching documents: 

	$ db.players.find( { team: “Miami Heat” }, { _id: 0, ‘name.first’: 0, conference: 0 } )

Ordering Documents 
Sorting documents in the find ( ) operation can be done using the sort ( ) method. This corresponds to the ORDER BY statement of  SQL. Here’s an example of ordering documents: 

	$ db.players.find( ).sort( { team: 1 } )

Limit the Number of Documents to Return 
You can also limit the number of documents to return in MongoDB using the limit ( ) method. In this following example, the query will limit the document to be returned only to 2 documents: 

	$ db.players.find( ).limit(2)

Set Starting Point of Result Set
You can also set the starting point of the result set of your query by using the skip ( ) method. In this example, the query will start the result set after the 5th document in your collection: 

	$ db.players.find( ).skip(5)

FindOne( ) method
The findOne( ) method works similar to the find( ) method, but it only returns a single document from a collection rather than everything it can find that matches the query and projection. It follows the syntax: 

	$ db.players.findOne( <query> , <projection> ) 

Update 
This basic operation modify existing records or documents in a MongoDB collection. MongoDB provides the following methods to perform update operations namely, update and save methods. 

The update ( ) Operation
The update ( ) method is the primary method used to modify documents in a MongoDB collection and by default it updates a single document. This method can update all documents that matches the query in the collection. This method can also replace the existing document with the new document or update specific fields in an existing document. The update method corresponds to the UPDATE operation in SQL. The update ( ) method follows the syntax: 

	$ db.collection.update( <query>, <update>, <options>)

Update a Field and Add a New Field to a Document
The <query> argument corresponds to the WHERE statement in SQL. The <update> corresponds to the SET statement in SQL. The <options> argument contains the multi option set.

	Ex: $ db.players.update({ _id: 1}, 
    { 
	$set : { position: “Shooting Guard”, aka: “The Black Mamba”, 
	number: 24 } 
     })
In the example above, we are updating the information on the number field of this certain document, changing it from the value of 8 to the new value of 24. In this example also, we are updating the document as adding another field named position and aka with some values too. 


Remove a Field from a Document 
If the update method can add a field to a document, you can also remove a field from a document using the $unset operator. Take a look at an example below: 

	Ex: $ db.players.update({ _id: 1 }, { $unset: { college: 1 } })
The save ( ) method updates an existing document or inserts a document depending on the _id field of the document. This method is equivalent to the update ( ) method with the upsert option and a <query> argument on the _id field. It follows the syntax: 
> 
	$ db.players.save( <document> )
If the <document> argument contains the _id field that exists in the collection, the save ( ) method performs an update that replaces the existing document with the  <document> argument. The following example queries the players collection for a document where the _id equals ObjectId("505a4c148fafa712d99d0012") and replaces the document with the <document> argument: 

	$ db.players.save( { ObjectId("505a4c148fafa712d99d0012"), 
       name:  {first: “Tim”, last: “Duncan”, team: “San Antonio Spurs”  }
    })

Updating Arrays
Update an Element by Specifying Its Position
If the update operation requires an update of an element in an array field, the update ( ) method can perform the update using the position of the element and dot notation. Arrays in MongoDB are zero-based. The following operation queries the players collection for the first document with _id field equal to 1 and updates the second element in the awards array: 

	$ db.players.update( { _id: 1 }, { $set: { ‘awards.1’ : ‘Rookie of the Year’ }} )
Update an Element without Specifying Its Position 
The update ( ) method can perform the update using the $ positional operator if the position is not known. The array field must appear in the query argument in order to determine which array element to update. The following example queries the players collection for the first document where the _id equals ObjectId("51611adfd1c66104e5456985") and the awards array contains an element equal to Best Center. If found, the update ( ) method updates the first matching element in the array to Best Center of the Year: 

	$ db.players.update( { _id: ObjectId("51611adfd1c66104e5456985"), ‘awards’ : ‘Best Center’ }, 
          { $set: { ‘awards.$’ : ‘Best Center of the Year’ } } ) 

Add an Element to an Array 
The following operation queries the players collection for the first document that has an _id field equal to ("51611adfd1c66104e5456985") and adds a new element to the awards field: 
	
	$ db.players.update({ _id: ObjectId("51611adfd1c66104e5456985") }, 
         { $push: { awards : {"KIA Top Score Leaders 2013"}  } } )

Replace Existing Document with New Document 
If the <update> argument contains only field and value pairs, the update ( ) method replaces the existing document with the document in the <update> argument, except for the _id field because it is immutable. 

	$ db.players.update( { name: { first: “Kobe”, last: “Bryant”  } }, 
          { name: { first: “Dwight”, last: “Howard”}, 
birthdate: new Date(‘Jan 06, 1986’), 
awards: [“Best Center 2012”, “Best Defensive Player 2012”] 
        })

update ( ) Operations with the upsert Flag 
If you set the upsert option in the  <options> argument to true or 1 and no existing document match the <query> argument, the update ( ) method can insert a new document into the collection. This operation was already discussed in the insert operation early as a part of this tutorial. For the sake of categorizing it the method in the update core function it is stated again here, look at the example: 

	$ db.players.update({ name: {first: “Kobe”, last: “Bryant”} },
         { awards: [“5-time MVP award”, “4th Best All-time scorer”] },
         { upsert: true } )



Save

The save ( ) method updates an existing document or inserts a document depending on the _id field of the document. The save ( ) method is equivalent to update ( ) method with the upsert option and a <query> argument on the _id field. It has the syntax: 

	$ db.collection.save( <document> )
Save Performs an Update 
If the <document> argument contains the _id field that exists  in the collection, the save ( ) method performs an update that replaces the existing document with the <document> argument.

	Ex:  $ db.players.save( { _id: ObjectId("507c4e138fada716c89d0014"), 
	 name: { first: “Derrick”, last: “Rose” }, team : “Chicago Bulls”, 
	position: “Point Guard”, conference: “Eastern”, years_pro: 6 })

Delete 

The delete ( ) Operation
Of the four basic operations, delete operations are those that remove documents from a collection in MongoDB. Use the remove ( ) method to delete documents from a collection. The remove ( ) method is analogous to the DELETE statement in SQL. This method follows the syntax: 

	$ db.players.remove( <query>, <justOne> )
As you can see in the syntax, the <query> argument corresponds to the WHERE statement in SQL, and the <justOne> argument takes a Boolean and has the same affect as LIMIT1. Take note, if you did not specify a query, remove ( ) method removes all documents from a collection, but does not remove the indexes. If there is a <query> argument, the remove ( ) method deletes from the collection all document that match the argument. In this next example, the operation deletes all documents from the players collection where the subdocument name contains a field last whose values starts with L: 

	$ db.players.remove( { ‘name.last’ : /^L/ } )
However, if there is a <query> argument and you specify the <justOne> argument as true or 1, the remove ( ) method only deletes a single document from the collection that matches the query. The following operation deletes a single document from the players collection where the college field equal true: 

	$ db.players.remove ({ college: true }, 1)
References Used:
 
http://docs.mongodb.org/manual/reference/sql-aggregation-comparison/ 
http://docs.mongodb.org/manual/reference/sql-comparison/ 
http://docs.mongodb.org/manual/crud/ 
http://www.mkyong.com/mongodb/how-to-create-database-or-collection-in-mongodb/ 

Tutorial pages done by: Ralph
