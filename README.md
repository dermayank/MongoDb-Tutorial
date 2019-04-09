# MongoDB-Tutorial

### Starting & Stopping

`$sudo service mongod start` starts the mongodb server

`$sudo service mongod stop` stops the mongodb server

`$sudo service mongod restart` restarts the mongodb server

`$mongo`  starts the shell

---

### Basics

`>db.help()` returns the lists of command

`>db.stats()` returns the stats about the MongoDB client. 

`>use database_name` it will create a new database or return if the database already exists.

`>db` will return the name of current database

`>show dbs` returns the list of all the availabel databases with there size

`>db.dropDatabase()` it will delete the current database

---

### Collections

**Collections:** is a group of MongoDB documents. It is the equivalent of an RDBMS table. A collection exists within a single database. Collections do not enforce a schema. Documents within a collection can have different fields.

`>db.createCollection(ct_name, options)` It creates a new collection with name as ct_name.


**Options:** Specify options about memory size and indexing. This is an optional parameter.

| Field         | Type     |
| ------------ | -------- |
| capped        | Boolean  |
| autoIndexID   | Boolean  |
| size          | number   |
| max           | number   |
		

`>show collections`	displays the list of all the available collections

`>db.ct_name.drop()` drops the collection with the name as *ct_name*

---

### Insertion 

`>db.ct_name.insert(document)`  inserts the document into the collection *ct_name*. We can pass a single document or an array of document in a query. 											\_id is optional, but is specifed must be unique for every document.  
	

		Example of single document insertion in mongodb
		```
			   >db.mycol.insert({
				   _id: ObjectId(7df78ad8902c),
				   title: 'MongoDB single query', 
				   description: 'MongoDB is no sql database',
				   tags: ['mongodb', 'database', 'NoSQL']
				})
		```

		Example of multiple document insertion in mongodb
		```
			      >db.mycol.insert([
				   {
				      title: 'MongoDB Overview', 
				      description: 'MongoDB is no sql database',
				      tags: ['mongodb', 'database', 'NoSQL'],
				   },
					
				   {
				      title: 'NoSQL Database', 
				      description: "NoSQL database doesn't have tables",
				      likes: 20, 
				      comments: [
				         {
				            user:'user1',
				            message: 'My first comment'
				         },
				         {
				            user:'user2',
				            message: 'My second comment'
				         }
				      ]
				   }
				])
		```

---

### Search

`>db.ct_name.find()`  will display all data in non-structured way. It is similar to *select * from table_name* query in sql.

`>db.ct_name.find().pretty()` will display all data just like above but in strucutred way.

\_id  will always be displayed with the find operation. To disable it, we need to set it to 0. Ex: *db.ct_name.find({},{_id=0}).pretty()*

| Operation            | Syntax                     |Example 												| Equivalent		|
| -------------------  | ------------------------- | ------------------------------------------------ 		| ---------------- |
| Equality             |  {\<key>: \<value>}          |  db.ct_name.find({"name": "mayank"}).pretty()		|   name = mayank	|
| Less than            |  {\<key>: {$lt: \<value>}}    |  db.ct_name.find({"age": {$lt: 100}}).pretty()		|	age < 100		|
| Less than equals     |  {\<key>: {$lte: \<value>}}   |  db.ct_name.find({"age": {$lte: 10}}).pretty()		|	age <= 100		|
| Greater than         |  {\<key>: {$gt: \<value>}}	|  db.ct_name.find({"age": {$gt: 50}).pretty()			|	age > 50		|
| Greater than equals  |  {\<key>: {$gte: \<value>}}	|  db.ct_name.find({"age": {$gte:70}}).pretty()			|	age >= 50		|
| Not Equals		   |  {\<key>: {$ne: \<value>}}	|  db.ct_name.find({"age": {$ne: 50}}).pretty()			|	age != 50		|
| AND 				   |  {$and: [{\<key1>: \<value1>},{\<key2>: \<value2>}]} | db.ct_name.find({$and: [{age:15},{likes:12}]).pretty()	|	age=15 and likes=12	|
| OR 				   |  {$or: [{\<key1>: \<value1>},{\<key2>: \<value2>}]}	| db.ct_name.find({$or: [{age:15},{likes:12}]).pretty() |	age=15 or likes=12	|


		'''
			Select documet with either (name = mayank) or (time =1 and tags = 3)
				>db.test_db.find({$or:
					[{name:"mayank"},{
						$and:[{"time":1},
						{tags:3}]
						}
					]
				}).pretty()
		'''
---

### Update

`>db.ct_name.update(selection_criteria, updation_criteria)`	updation can be performed using *update()* and *save()* methods. *update()* method updates the value in existing documents while *save()* method replaces the existing documents with the one passed in save() method.

We always specify `$set` in updation criteria. The `$set` operator replaces the value of a field with the specified value.

		'''
			Updates the parameter age with value 22
			 >db.test_db.update({"name":"mayank joshi"},
			 		{$set:{"age":22}
			 	},{multi:true})

			 Adds and additional value address with value to the record matching the name parameter as "mayank joshi"
			 >db.test_db.update({"name":"mayank joshi"},
			 		{$set:{"address":"newly added address"}
			 	})
		''' 

By default the `update()` operation will only update a single document or record. To update multiple the documents we need to set parameter `multi` to *true*


