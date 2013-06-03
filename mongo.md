Mongo
=====

[Mongo DB](http://docs.mongodb.org/manual/) is a database used to store and query JSON-style "documents".


## Basic Hierarchy

    database 
      collection
        document 
          field 
            key:value

A *collection* is analogous to a (relational database's) table and a *document* to a row within a table.


## Conditional query operators

* `$lt` - less than
* `$gt` - greater than
* `$lte` - less than or equal
* `$gte` - greater than or equal
* `$ne` - not equal
* `$in` - is in array
* `$nin` - is not in array

Example: `db.people.find({ age: {$gt:21} })`


## The Shell

The `mongo` shell is in fact a full-fledged javascript REPL.  You can thus use the shell to build javascript objects on the fly before storing them, or selectively pull and manipulate some JSON before re-persisting.

Use `help` for an overview of the built-in docs. Full documentation available in the [manual](http://docs.mongodb.org/manual/mongo/#the-mongo-shell)

You can actually view the built in method definitions by leaving off the parens (for method invocation).  For example, try `db.collection.find` (instead of `db.collection.find()`) to see the *find()* method's argument parameters and definition.

The [getting-started tutorial](http://docs.mongodb.org/manual/tutorial/getting-started/) provides a quick overview of Mongo via the shell. The [@hacksparrow tutorial](http://www.hacksparrow.com/the-mongodb-tutorial.html) goes a bit further in introducing the basics.

Example session:

    > show dbs
    local 0.078125GB
    > use gov
    switched to db gov
    > show collections

With `use gov` we're implictly creating and selecting an empty database.  It does not yet contain any collections.  Once a database is selected it is referenced via `db`.

    > db.getName()
    gov

Let's add a new collection (`presidents`) and insert some documents.

    > db.presidents.insert( { number: 1, name: "Washington", begin: 1789, end: 1797 } )
    > db.presidents.insert( { number: 2, name: "Adams", begin: 1797, end: 1801 } )
    > db.presidents.insert( { number: 3, name: "Jefferson", begin: 1801, end: 1809 } )
    > db.presidents.insert( { number: 4, name: "Madison", begin: 1809, end: 1817 } )

Note that our `gov` database shows up in the list of available databases now that it has some actual content.

    > show dbs
    gov 0.203125GB
    local 0.078125GB

Since `db` is the selected database we can list its collections with `show`.

    > show collections
    presidents
    system.indexes

Alternatively ...

    > db.getCollectionNames()
    presidents
    system.indexes

We can use the `save` method to update a document.

    > madison = { "_id" : ObjectId("519e6c76b4ee970a31eb47f6"), "number" : 4, 
    "name" : "Madison", "begin" : 1809, "end" : 1817 }
    > madison.end = 1813
    > db.presidents.save(madison)
    > db.presidents.find({ name: "Madison" })
    { "_id" : ObjectId("519e6c76b4ee970a31eb47f6"), "number" : 4, "name" :
    "Madison", "begin" : 1809, "end" : 1813 }

Reverting back.

    > madison.end = 1817
    > db.presidents.save(madison)
    > db.presidents.find({ name: "Madison" })
    { "_id" : ObjectId("519e6c76b4ee970a31eb47f6"), "number" : 4, "name" :
    "Madison", "begin" : 1809, "end" : 1817 }

Let's query the collection.

    > db.presidents.find()
    { "_id" : ObjectId("519e6c29b4ee970a31eb47f3"), "number" : 1, 
    "name" : "Washington", "begin" : 1789, "end" : 1797 }
    { "_id" : ObjectId("519e6c45b4ee970a31eb47f4"), "number" : 2, 
    "name" : "Adams", "begin" : 1797, "end" : 1801 }
    { "_id" : ObjectId("519e6c61b4ee970a31eb47f5"), "number" : 3, 
    "name" : "Jefferson", "begin" : 1801, "end" : 1809 }
    { "_id" : ObjectId("519e6c76b4ee970a31eb47f6"), "number" : 4, 
    "name" : "Madison", "begin" : 1809, "end" : 1817 }

Limiting to 2 results.

    > db.presidents.find().limit(2)
    { "_id" : ObjectId("519e6c29b4ee970a31eb47f3"), "number" : 1, 
    "name" : "Washington", "begin" : 1789, "end" : 1797 }
    { "_id" : ObjectId("519e6c45b4ee970a31eb47f4"), "number" : 2, 
    "name" : "Adams", "begin" : 1797, "end" : 1801 }

Return one result.

    > db.presidents.findOne()
    {
      "_id" : ObjectId("519e6c29b4ee970a31eb47f3"),
      "number" : 1,
      "name" : "Washington",
      "begin" : 1789,
      "end" : 1797
    }

We can query for all documents with specifc attributes.

    > db.presidents.find({ name: "Jefferson" })
    { "_id" : ObjectId("519e6c61b4ee970a31eb47f5"), "number" : 3, 
    "name" : "Jefferson", "begin" : 1801, "end" : 1809 }

We can use conditional queries as well.

    > db.presidents.find({ end: {$lt:1808} })
    { "_id" : ObjectId("519e6c29b4ee970a31eb47f3"), "number" : 1, 
    "name" : "Washington", "begin" : 1789, "end" : 1797 }
    { "_id" : ObjectId("519e6c45b4ee970a31eb47f4"), "number" : 2, 
    "name" : "Adams", "begin" : 1797, "end" : 1801 }
    > db.presidents.find({ begin: {$gt:1800} })
    { "_id" : ObjectId("519e6c61b4ee970a31eb47f5"), "number" : 3, 
    "name" : "Jefferson", "begin" : 1801, "end" : 1809 }
    { "_id" : ObjectId("519e6c76b4ee970a31eb47f6"), "number" : 4, 
    "name" : "Madison", "begin" : 1809, "end" : 1817 }


