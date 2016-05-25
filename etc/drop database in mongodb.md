# Drop database in MongoDB
Use ``db.dropDatabase()`` to delete the current selected database. If no database selected this 
commend will delete the default database ``test``. Before deleting you need show all database. 
Delete a database commend like following.
```bash
> show dbs
local          0.078GB
new_database   0.078GB
user_database  0.078GB
> use user_database
switched to db user_database
> db.dropDatabase()
{ "dropped" : "user_database", "ok" : 1 }
> db
user_database
```
As you can see after executing ``db.dropDatabase()`` the database ``user_database`` is still there.
If you execute ``db.users.insert()``, the database ``user_database`` will "come back". But, switch to
other database before inserting data ``user_database`` will disappear unless you create it again.