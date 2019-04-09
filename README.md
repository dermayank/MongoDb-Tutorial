# MongoDB-Tutorial

### Starting & Stopping

`sudo service mongod start`	starts the mongodb server

`mongo`  starts the shell

`sudo service mongod stop` 	stops the mongodb server

---

### Basics

`db.help()`	returns the lists of command

`db.stats()` returns the stats about the MongoDB client. 

`use database_name` it will create a new database or return if the database already exists.

`db` will return the name of current database

`show dbs` returns the list of all the availabel databases with there size

`db.dropDatabase()` it will delete the current database

---

### Collections

**Collection** is a group of MongoDB documents. It is the equivalent of an RDBMS table. A collection exists within a single database. Collections do not enforce a schema. Documents within a collection can have different fields.

`db.createCollection(ct_name, options)` It creates a new collection with name as ct_name.

---

**Options:** Specify options about memory size and indexing. This is an optional parameter.
		
		 Field | Type	
		 --- | --- | ---	
		 capped | Boolean		
		 autoIndexId | Boolean
		 size | number
		 max | number

`show collections`	displays the list of all the available collections

`db.COLLECTION_NAME.drop()` drops the collection with the name as COLLECTION_NAME

---

### Insertion 


