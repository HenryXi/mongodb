# Update null or not exist field in MongoDB
Use `db.collection.update` to update the document. Do not know how to update document you can click [Update document in MongoDB](http://www.henryxi.com/update-document-in-mongodb).
In this page I will show you how to update document which field is null or not exists.

If this field is null update it like following. (I do not recommend set value to null. If the value is null you
can delete this key.)
```bash
> db.user.find()
{ "_id" : ObjectId("5761de0edd74253dfbb00591"), "_class" : "com.henryxi.mongo.template.User", "name" : null, "age" : 27 }
{ "_id" : ObjectId("5761de0edd74253dfbb00594"), "_class" : "com.henryxi.mongo.template.User", "name" : "new Charles", "age" : 32, "address" : { "country" : "China", "city" : "Beijing" } }
> db.user.update({"name": null}, {"$set": {"name": "Henry"}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
> db.user.find()
{ "_id" : ObjectId("5761de0edd74253dfbb00591"), "_class" : "com.henryxi.mongo.template.User", "name" : "Henry", "age" : 27 }
{ "_id" : ObjectId("5761de0edd74253dfbb00594"), "_class" : "com.henryxi.mongo.template.User", "name" : "new Charles", "age" : 32, "address" : { "country" : "China", "city" : "Beijing" } }
```
If this field do not exist update it like following.
```bash
> db.user.find()
{ "_id" : ObjectId("5761de0edd74253dfbb00591"), "_class" : "com.henryxi.mongo.template.User", "name" : "Henry", "age" : 27 }
{ "_id" : ObjectId("5761de0edd74253dfbb00594"), "_class" : "com.henryxi.mongo.template.User", "name" : "new Charles", "age" : 32, "address" : { "country" : "China", "city" : "Beijing" } }
> db.user.update({"company": {"$exists": false}}, {"$set": {"company": "The company"}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
> db.user.find()
{ "_id" : ObjectId("5761de0edd74253dfbb00591"), "_class" : "com.henryxi.mongo.template.User", "name" : "Henry", "age" : 27, "company" : "The company" }
{ "_id" : ObjectId("5761de0edd74253dfbb00594"), "_class" : "com.henryxi.mongo.template.User", "name" : "new Charles", "age" : 32, "address" : { "country" : "China", "city" : "Beijing" } }
```
`db.collection.update` will only update the first document if you do not set `{multi:true}`.
