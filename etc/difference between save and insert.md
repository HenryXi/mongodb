# Difference between save and insert in MongoDB
Insert data into MongoDB is very easy. In this page I will tell you the difference between save method and insert 
method in MongoDB. If you don't know how to insert data into MongoDB you can see this blog([Insert data in MongoDB](http://www.henryxi.com/insert-data-in-mongodb)).
To put it simply, save method will call insert or update method. It is depends on the data you saved contain the `_id`
or not. If the data you saved contain the `_id` save method will call update method. If not it will call insert
method. Examples are here.
```bash
> db.user.save({name:"Henry"})
WriteResult({ "nInserted" : 1 })
> db.user.findOne()
{ "_id" : ObjectId("575f6ec5f045569ea421c495"), "name" : "Henry" }
```
MongoDB will generate `_id` for every document if it do not have one. If you save this document again(without `_id`)
MongoDB will save it as a new document.
```bash
> db.user.find({})
{ "_id" : ObjectId("575f6ec5f045569ea421c495"), "name" : "Henry" }
{ "_id" : ObjectId("575f6fa3f045569ea421c496"), "name" : "Henry" }
```
If you save the document with `_id` and this id exist in MongoDB save method will call update method to update
this document.
```bash
> db.user.save({"_id":ObjectId("575f6ec5f045569ea421c495"),name:"new Henry"})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
> db.user.find({})
{ "_id" : ObjectId("575f6ec5f045569ea421c495"), "name" : "new Henry" }
{ "_id" : ObjectId("575f6fa3f045569ea421c496"), "name" : "Henry" }
```