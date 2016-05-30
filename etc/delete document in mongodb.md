# Delete document in MongoDB
Use `db.collection.remove()` method to delete document in MongoDB. You can define a query to make it
delete documents match query. How to define a query click [Query document in MongoDB](http://www.henryxi.com/query-document-in-mongodb). 
If you want remove all documents of this collection just use empty query to match all documents. MongoDB will delete 
all document of this collection.
```bash
> use user_database
switched to db user_database
> db.user.insert({name:"Henry"})
WriteResult({ "nInserted" : 1 })
> db.user.insert({name:"Xi"})
WriteResult({ "nInserted" : 1 })
> db.user.insert({name:"Justin",age:27})
WriteResult({ "nInserted" : 1 })
> db.user.find()
{ "_id" : ObjectId("574b822696af9dffe372c22b"), "name" : "Henry" }
{ "_id" : ObjectId("574b822b96af9dffe372c22c"), "name" : "Xi" }
{ "_id" : ObjectId("574b824096af9dffe372c22d"), "name" : "Justin", "age" : 27 }
> db.user.remove({name:"Henry"})
WriteResult({ "nRemoved" : 1 })
> db.user.find()
{ "_id" : ObjectId("574b826196af9dffe372c22e"), "name" : "Justin", "age" : 27 }
{ "_id" : ObjectId("574b826696af9dffe372c22f"), "name" : "Xi" }
> db.user.remove({})
WriteResult({ "nRemoved" : 2 })
```
Querying document before deleting is a good habit. This will prevent accidentally deleted documents.