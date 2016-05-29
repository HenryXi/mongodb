# Query document in MongoDB
In MongoDB `db.collection.find()` method query documents from the collection. If there is no param in
it or passing empty param like this `db.collection.find({})` will get all documents in this collection.
It is like using `select * from table_name` in structural database.
```bash
> db.user.find()
{ "_id" : ObjectId("5747b01d4bca08a38db22ad3"), "name" : "Henry" }
{ "_id" : ObjectId("5747b1562a9f793542c63acc"), "name" : "Xi" }
{ "_id" : ObjectId("5747b1562a9f793542c63acd"), "name" : "Justin", "age" : 27 }
{ "_id" : ObjectId("5747b8a12a9f793542c63ace"), "name" : "Mathew", "age" : 23, "address" : { "country" : "China", "province" : "Beijing" } }
```
If you want to query the document which name is "Xi". You can use the query document `{name:"Xi"}` or `{"name","Xi"}`.
```bash
> db.user.find({name:"Xi"})
{ "_id" : ObjectId("5747b1562a9f793542c63acc"), "name" : "Xi" }
> db.user.find({"name":"Xi"})
{ "_id" : ObjectId("5747b1562a9f793542c63acc"), "name" : "Xi" }
```
Query the document which name exist in the array. Following query find the document which name in `["Xi","Mathew"]`
```bash
> db.user.find({"name":{$in:["Xi","Mathew"]}})
{ "_id" : ObjectId("5747b1562a9f793542c63acc"), "name" : "Xi" }
{ "_id" : ObjectId("5747b8a12a9f793542c63ace"), "name" : "Mathew", "age" : 23, "address" : { "country" : "China", "province" : "Beijing" } }
```
Query the document with `AND` conditions. If there is no document match the condition MongoDB will return empty.
You can use `db.collection.count()` method to count the number of documents.
```bash
> db.user.find({name:"Justin",age:27})
{ "_id" : ObjectId("5747b1562a9f793542c63acd"), "name" : "Justin", "age" : 27 }
> db.user.find({name:"Justin",age:23})

> db.user.count({name:"Justin",age:23})
0
```
Query the document with `OR` conditions.
```bash
> db.user.find({$or:[{name:"Henry"},{age:27}]})
{ "_id" : ObjectId("5747b01d4bca08a38db22ad3"), "name" : "Henry" }
{ "_id" : ObjectId("5747b1562a9f793542c63acd"), "name" : "Justin", "age" : 27 }
```
For embedded document we can query like following. Do **not** lose dot in `"address.country"`   
```bash
> db.user.find({"address.country":"China"})
{ "_id" : ObjectId("5747b8a12a9f793542c63ace"), "name" : "Mathew", "age" : 23, "address" : { "country" : "China", "province" : "Beijing" } }
> db.user.find({"address.province":"Beijing"})
{ "_id" : ObjectId("5747b8a12a9f793542c63ace"), "name" : "Mathew", "age" : 23, "address" : { "country" : "China", "province" : "Beijing" } }
```
The result of query is not formatted. [Format query result in MongoDB]()