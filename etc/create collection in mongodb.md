# Create collection in MongoDB
You can create collection explicitly or make MongoDB help you create collection automatically. When you
create collection manually you can use specific options. You can create a capped collection or create a collection
with document validation.

**create collection automatically**

When you insert document in a collection which is not exist MongoDB will create collection automatically.
```lang-none
> show collections
system.indexes
> use user_database
switched to db user_database
> db.users.insert({'name':'test'})
WriteResult({ "nInserted" : 1 })
> show collections
system.indexes
users
```
**create collection manually**

You can also create collection manually by using following command(**case matters**). In this way you
 can create a capped
collection. 
```lang-none
> db.createCollection('test')
{ "ok" : 1 }
> show collections
system.indexes
test
users
```
There are some option parameters in create command. Click [here](https://docs.mongodb.com/manual/reference/method/db.createCollection/) for more detail.