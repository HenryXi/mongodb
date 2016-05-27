# Insert data in MongoDB
We need create table before inserting data into structure database(Mysql, PostgreSQL, Oracle etc.).
It is no need to create collection for using MongoDB. The `db.collection.insert()` method adds new
document into database. MongoDB will create collection when it not exist. You can also create collection 
manually then insert document.
```bash
> use user_database
switched to db user
> db.user.insert({"name":"Henry"})
WriteResult({ "nInserted" : 1 })
> db.user.find()
{ "_id" : ObjectId("5747b01d4bca08a38db22ad3"), "name" : "Henry" }
> db.user.insert([{"name":"Xi"},{"name":"Justin","age":27}])
BulkWriteResult({
	"writeErrors" : [ ],
	"writeConcernErrors" : [ ],
	"nInserted" : 2,
	"nUpserted" : 0,
	"nMatched" : 0,
	"nModified" : 0,
	"nRemoved" : 0,
	"upserted" : [ ]
})
> db.user.find()
{ "_id" : ObjectId("5747b01d4bca08a38db22ad3"), "name" : "Henry" }
{ "_id" : ObjectId("5747b1562a9f793542c63acc"), "name" : "Xi" }
{ "_id" : ObjectId("5747b1562a9f793542c63acd"), "name" : "Justin", "age" : 27 }
```
As you can see `db.collection.insert()` support insert one document or array of documents. After inserting
data MongoDB return `WriteResult` or `BulkWriteResult`. `nInserted` in them means how many documents were
inserted successfully. If there are any errors during the inserting `WriteResult` with `writeConcernError` 
will return.