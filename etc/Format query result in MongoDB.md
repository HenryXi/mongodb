# Format query result in MongoDB
The default result of querying document in MongoDB is not formatted. But if you query one document by
using `db.collection.findOne()` the result is formatted. Is there any way to format the result of `db.collection.find()`?
Yes, use `pretty()` append `db.collection.find()`. Examples are here.
```bash
> db.user.find({name:"Mathew"})
{ "_id" : ObjectId("5747b8a12a9f793542c63ace"), "name" : "Mathew", "age" : 23, "address" : { "country" : "China", "province" : "Beijing" } }
> db.user.find({name:"Mathew"}).pretty()
{
	"_id" : ObjectId("5747b8a12a9f793542c63ace"),
	"name" : "Mathew",
	"age" : 23,
	"address" : {
		"country" : "China",
		"province" : "Beijing"
	}
}
```
The result of `db.collection.findOne()` is formatted by default.
```bash
{ "_id" : ObjectId("5747b01d4bca08a38db22ad3"), "name" : "Henry" }
> db.user.findOne({name:"Mathew"})
{
	"_id" : ObjectId("5747b8a12a9f793542c63ace"),
	"name" : "Mathew",
	"age" : 23,
	"address" : {
		"country" : "China",
		"province" : "Beijing"
	}
}
```