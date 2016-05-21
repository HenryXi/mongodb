# Create Database in MongoDB
In MongoDB you do not need create database manually. MongoDB will create a new database if necessory. It is different
from structure database. Open Mongo shell and type ``show dbs`` can show all database. Now there is only one database
(local) in my computer.
```bash
MongoDB shell version: 3.2.5
connecting to: localhost:27017/test
> show dbs
local  0.078GB
```
Use ``use <new_database_name>`` command to switch database if you want save your data in this database.
But now the new database is not created. **The database is created when you insert some data in any 
collection of it**. Try to run the commands like following.
```bash
> use new_database
switched to db new_database
> db.testCollection.insert({"name":"test"});
WriteResult({ "nInserted" : 1 })
```
When you add documents to a collection that does not exist, MongoDB will create it automatically. You
can also create collection manually. I will show you how to create collection in next blog.
Now the database is created successfully. Use ``show dbs`` you will get the result as following.
```bash
> show dbs
local         0.078GB
new_database  0.078GB
```
