---
layout: post
title: "NodeJS & Databases: MongoDB"
comments: true
publish: true
---

As already mentioned, databases are typically a key component of back-end architecture. Luckily, NodeJS, which enables us to run server-side JavaScript code, can connect to several of the major database server engines.

MongoDB is another database option that is very popular to use with NodeJS. 

## Background

MongoDB started being developed by 10gen (later MongoDB Inc.) around 2007. It is the most widely used open-source non-relational database engine. This type of database is also often referred to as NoSQL or as a document store.

The NoSQL moniker refers to a departure from the traditional table/row/column approach. Instead, all data is stored in JSON format. (MongoDB calls it BSON.) NoSQL database engines also use a dynamic schema, as opposed to a pre-defined table structure, and are commonly used to house large volumes of information. Hence the term Big Data, and hence huMONGOus.


## Some Terminology

In the NoSQL world, databases are still called databases, but tables are termed collections and records, documents.

Terminology aside, the stark difference, especially for someone coming from an SQL background, is that everything in MongoDB is in JSON format, right down to the database command arguments themselves, as opposed to the natural language constructs of SQL. This takes some getting used to.


## Installation, Set-up & Shell

### Cloud9 IDE
Each C9 workspace comes with MongoDB already installed, so there's nothing to install per se. However, as things stand right now, you do need to create a start-up file. 

To create a start-up file:

-- `Alt-t` to open a terminal tab.

-- Type in `echo 'mongod --nojournal' > mongod`.

-- Then type in `chmod 777 mongod`.

-- You're done with this terminal tab and you can close it.


To start the database server:

-- `Alt-t` then type in `./mongod`. 

-- Keep this tab open, with this command running.

-- To get a command line shell, open a second terminal tab and type in `mongo`.
    

The installed MongoDB that comes with each C9 workspace is version 2.x. It's recommended that you update to version 3.x, and for instructions on how to do this you may copy and run the `mongo-update` file in the [repo](https://github.com/lcarbonaro/nodejs/blob/master/session29/mongo-update), or refer to [this post](https://community.c9.io/t/updating-mongodb/3914) in the C9 docs.


### Windows

-- Download the relevant version from the [MongoDB site](https://www.mongodb.org/) and install.
 
-- In a command window do a `mkdir /data/db` (This is the default db path that MongoDB expects.)
 
-- Then `mongod` to start the MongoDB database server. (You may need to go to mongodb\bin folder first, if it's not in your Windows path.)

-- Keep this window open, with this command running.

-- To get a command line shell, open a second command window and type in `mongo`. (Again, you may need to be in mongodb\bin first.)

### Mac
Installation and set-up is presumably similar to Windows. 

Note that you might need `sudo` to start the database server and shell command line.


## Some example shell commands:

### To show/create/use databases:

To show databases: `show dbs`

To switch to a particular database: `use test`

Note that this will create the database if it does not exist already.


### To create a collection:

To show collections in a database: `show collections`

To create a new collection: `db.createCollection('category')`

Remember that a collection is like a table in the SQL world. Notice also that we do not declare structure (fields, field types, etc.) as part of creating a new collection, like we did in SQL with `create table...`. This is what is meant by MongoDB having a dynamic schema. In fact it is perfectly fine to have documents (records) with different fields within the same collection.


### To insert documents:

To insert documents into a collection, use the `insertOne` and `insertMany` methods on the collection name, for example:

`db.category.insert({"name":"Groceries"})`

`db.category.insert( [ {"name":"Rent"} , {"name":"Medical"} ] )`

Notice the JSON format of the arguments to the `insert` method.


### To retrieve documents:

To fetch documents from a collection, use the `find` method on the collection name, for example:

`db.category.find()`

> { "_id" : ObjectId("572..ff2"), "name" : "Groceries" }

> { "_id" : ObjectId("572..ff3"), "name" : "Rent" }

> { "_id" : ObjectId("572..ff4"), "name" : "Medical" }


Without any arguments, the `find` method returns all the documents in the collection. Notice that MongoDB automatically assigned a unique id. to each document.


`db.category.find( { "name": { "$eq" : "Rent" } } )`

> { "_id" : ObjectId("572..ff3"), "name" : "Rent" }

Notice the `$eq` operator. This would be the equivalent to SQL: 

{% highlight sql %}
select * from `category` where `name` = 'Rent'
{% endhighlight %}

The `find` method can take a second argument, which specifies the fields we wish to include or exclude in the result, for example:

`db.category.find( { "name":{"$eq":"Medical"} } , { "name":1,"_id":0 } )`

> { "name" : "Medical" }

In the [MongoDB manual](https://docs.mongodb.com/manual/reference/method/db.collection.find) you will find more extensive details and usage examples for the `find` method.


### To update documents:

To update documents in a collection, use the `update` method on the collection name.

The `update` method may take three arguments:

-- query: which documents are to be updated

-- update: what fields are to be updated

-- options: such as `multi` (update multiple documents), or `upsert` (insert if no match found)

For example:

{% highlight javascript %}
db.category.update(
  { "name" : "Transport" },
  { "$set" : { "abbr": "TRN" , 
               "desc":"Bus tickets and cab fares" 
             } 
  },
  { "upsert" : true}
)
{% endhighlight %}

The `update` method can also be used to insert detail records (as in a master-detail or one-to-many relation), for example: 

{% highlight javascript %}
db.category.update ( 
  { "name" : "Groceries" }, 
  { $push: { expenses: { amount: 22.50 } } } 
)
{% endhighlight %}


Contrast this with the relational database approach, where we created two separate tables (`category` and `expense`) and then used a `left outer join` to connect the two on a foreign key.


In the [MongoDB manual](https://docs.mongodb.com/manual/reference/method/db.collection.update) you will find more details and examples for the `update` method.



### To delete documents:


To delete documents in a collection, we can use the `remove` method on the collection name.

The `remove` method may take two arguments:

-- query: which documents are to be deleted

-- options: such as `justOne` (delete only one document not all documents that match)

For example:

`db.category.remove( { 'name' : {"$regex":".*t"} } )`

Note that passing in an empty query option will delete all documents in the collection.


In the [MongoDB manual](https://docs.mongodb.com/manual/reference/method/db.collection.remove/) you will find more details and examples for the `remove` method.


This covers the basics of the basic CRUD operations in MongoDB. 

This [github repo](https://github.com/lcarbonaro/nodejs/tree/master/session32) gives a simple example of how to use MongoDB from within a NodeJS application.



## References &amp; Resources

- [More on NoSQL](https://www.mongodb.com/nosql-explained)
- [MongoDB Wikipedia entry](https://en.wikipedia.org/wiki/MongoDB)
- [MongoDB official docs](https://docs.mongodb.com/manual/)
- [MongoDB for NodeJS (npm module docs)](https://www.npmjs.com/package/mongodb)
- [MongoDB tutorial](http://www.tutorialspoint.com/mongodb/index.htm)
- [MongoDB University (free online courses)](https://university.mongodb.com/)
- [Github Repo](https://github.com/lcarbonaro/nodejs/tree/master/session29)