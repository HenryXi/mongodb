# Create Database in MongoDB
In MongoDB you do not need create database manually. MongoDB will create a new database if necessory. It is different
from structure database. Open Mongo shell and type ``show dbs`` can show all database. Now there is only one database
(local) in my computer.
```
MongoDB shell version: 3.2.5
connecting to: localhost:27017/test
> show dbs
local  0.000GB
```
Use ``use <database_name>`` command to switch database if you want save your data in a new database.  
