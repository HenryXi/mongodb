# Drop collection in MongoDB
Drop collection in MongoDB is easy. Use ``db.collection_name.drop()`` to drop the collection. All indexes
 in this collection will be also removed.  
```bash
> show collections
system.indexes
test
users
> db.test.drop()
true
> show collections
system.indexes
users
```
One thing to note here is that this command will obtains a write lock on the database. Other operations
will be blocked until drop command has completed.
