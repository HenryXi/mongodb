# Update document in MongoDB
We use `db.collection.update()` to update the document. Since version 3.2 you can use `db.collection.updateOne()`
,`db.collection.updateMany()` or `db.collection.replaceOne()` to update document or documents. Click
[here](https://docs.mongodb.com/manual/tutorial/update-documents/) for more detail. In this page I will
show you sample examples.

```
> db.user.save([{"name":"Justin","age":NumberInt(27)},{"name":"Henry","age":NumberInt(27)},{"name":"Charles","age":NumberInt(35)},{"name":"Matthews","age":NumberInt(21)}])
BulkWriteResult({
	"writeErrors" : [ ],
	"writeConcernErrors" : [ ],
	"nInserted" : 4,
	"nUpserted" : 0,
	"nMatched" : 0,
	"nModified" : 0,
	"nRemoved" : 0,
	"upserted" : [ ]
})
```

update Charles's age
```
> db.user.findOne({name:"Charles"})
{
	"_id" : ObjectId("576ded03c1e5b2a01edf3c10"),
	"name" : "Charles",
	"age" : 35
}
> db.user.update({"name":"Charles"},{$set:{"age":NumberInt(32)}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
> db.user.findOne({name:"Charles"})
{
	"_id" : ObjectId("576ded03c1e5b2a01edf3c10"),
	"name" : "Charles",
	"age" : 32
}
```

`db.collection.update()` will update the first document which match the filter. If you want update
multi documents use `multi` option.

update document which age is 27
```
> db.user.find({age:27})
{ "_id" : ObjectId("576ded03c1e5b2a01edf3c0e"), "name" : "Justin", "age" : 27 }
{ "_id" : ObjectId("576ded03c1e5b2a01edf3c0f"), "name" : "Henry", "age" : 27 }
> db.user.update({"age":27},{$set:{"age":NumberInt(32)}},{multi:true})
WriteResult({ "nMatched" : 2, "nUpserted" : 0, "nModified" : 2 })
> db.user.find({})
{ "_id" : ObjectId("576ded03c1e5b2a01edf3c0e"), "name" : "Justin", "age" : 32 }
{ "_id" : ObjectId("576ded03c1e5b2a01edf3c0f"), "name" : "Henry", "age" : 32 }
{ "_id" : ObjectId("576ded03c1e5b2a01edf3c10"), "name" : "Charles", "age" : 32 }
{ "_id" : ObjectId("576ded03c1e5b2a01edf3c11"), "name" : "Matthews", "age" : 21 }
```

use `$unset` to remove field when update
```
> db.user.update({"name":"Henry"},{$unset:{"age":""}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
> db.user.find({})

{ "_id" : ObjectId("576ded03c1e5b2a01edf3c0e"), "name" : "Justin", "age" : 32 }
{ "_id" : ObjectId("576ded03c1e5b2a01edf3c0f"), "name" : "Henry" }
{ "_id" : ObjectId("576ded03c1e5b2a01edf3c10"), "name" : "Charles", "age" : 32 }
{ "_id" : ObjectId("576ded03c1e5b2a01edf3c11"), "name" : "Matthews", "age" : 21 }
```