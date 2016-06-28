# Count document in MongoDB
Use `db.collection.count()` to count the number of documents. You can add a query filter to count the specific
documents. Examples are here.
```bash
> db.user.find()
{ "_id" : ObjectId("5761de0edd74253dfbb00591"), "_class" : "com.henryxi.mongo.template.User", "name" : "new Henry", "age" : 27 }
{ "_id" : ObjectId("5761de0edd74253dfbb00594"), "_class" : "com.henryxi.mongo.template.User", "name" : "new Charles", "age" : 32, "address" : { "country" : "China", "city" : "Beijing" } }
> db.user.count()
2
> db.user.count({name:"new Henry"})
1
```
If you do not know how to query document you can click [Query document in MongoDB](http://www.henryxi.com/query-document-in-mongodb).