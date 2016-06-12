# Create and drop index in MongoDB
Using `db.collection.createIndex(keys, options)` to create index for a field. If you want create an 
ascending index on a filed you need specify a value of 1; for descending index use -1. Examples are 
here.
```bash
> db.user.createIndex({name:1}) 
{
	"createdCollectionAutomatically" : false,
	"numIndexesBefore" : 1,
	"numIndexesAfter" : 2,
	"ok" : 1
}
> db.user.createIndex({age:-1})
{
	"createdCollectionAutomatically" : false,
	"numIndexesBefore" : 2,
	"numIndexesAfter" : 3,
	"ok" : 1
}
```
We create two indexes in user collection. When we query document with condition the index will 
improve query efficiency.
You can drop index by using `db.collection.dropIndex(index)`. Examples are here. If you don't know the 
index name you can use `db.collection.getIndexes()` to query all indexes in this collection.
```bash
> db.user.getIndexes()
[
	{
		"v" : 1,
		"key" : {
			"_id" : 1
		},
		"name" : "_id_",
		"ns" : "user_database.user"
	},
	{
		"v" : 1,
		"key" : {
			"name" : 1
		},
		"name" : "name_1",
		"ns" : "user_database.user"
	},
	{
		"v" : 1,
		"key" : {
			"age" : -1
		},
		"name" : "age_-1",
		"ns" : "user_database.user"
	}
]
> db.user.dropIndex("name_1")
{ "nIndexesWas" : 3, "ok" : 1 }
> db.user.dropIndex("age_-1")
{ "nIndexesWas" : 2, "ok" : 1 }
> db.user.getIndexes()
[
	{
		"v" : 1,
		"key" : {
			"_id" : 1
		},
		"name" : "_id_",
		"ns" : "user_database.user"
	}
]
```