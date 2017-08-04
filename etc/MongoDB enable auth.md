# MongoDB enable auth
I assume you have installed MongoDB in your environment. The version of MongoDB in my computer is 3.4.6. There are 
two ways to enable auth in MongoDB, start mongod service with `--auth` or change the configuration file. In this page
I will show you the second one.

**Goal:** create two users for "MyDB", the one is "user_read"(only have read-only permission) and the other is "user_read_write"(have read and write permissions).

**Steps**

1. start mongo in default way (without auth).
```bash
# service mongod start
Starting mongod:                                           [  OK  ]
```
2. connect local mongo.
```bash
# mongo
MongoDB shell version v3.4.6
connecting to: mongodb://127.0.0.1:27017
MongoDB server version: 3.4.6
Server has startup warnings: 
2017-08-03T18:23:16.425+0800 I STORAGE  [initandlisten] 
2017-08-03T18:23:16.425+0800 I STORAGE  [initandlisten] ** WARNING: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine
2017-08-03T18:23:16.425+0800 I STORAGE  [initandlisten] **          See http://dochub.mongodb.org/core/prodnotes-filesystem
2017-08-03T18:23:16.755+0800 I CONTROL  [initandlisten] 
2017-08-03T18:23:16.756+0800 I CONTROL  [initandlisten] ** WARNING: Access control is not enabled for the database.
2017-08-03T18:23:16.756+0800 I CONTROL  [initandlisten] **          Read and write access to data and configuration is unrestricted.
2017-08-03T18:23:16.756+0800 I CONTROL  [initandlisten] 
> 
```
3. create two users in database "admin" (this database will be authentication database for these user)
```bash
> use admin
switched to db admin
> db.createUser(db.createUser( { user: "user_read", pwd: "admin_pwd", roles: [ { role: "userAdminAnyDatabase", db: "admin" } ] } ))
Successfully added user: {
	"user" : "admin",
	"roles" : [
		{
			"role" : "userAdminAnyDatabase",
			"db" : "admin"
		}
	]
}
```
4. create database "MyDB". If you want to know the detail of creating database in mongo click [here](http://www.henryxi.com/create-database-in-mongodb)
```bash
> use MyDB
switched to db MyDB
> db.myCollection.save({name:"henryxi"})
WriteResult({ "nInserted" : 1 })
> db.myCollection.find()
{ "_id" : ObjectId("59846a3aba13b68481f3f54a"), "name" : "henryxi" }
```
5. change the configuration file to enable auth
Comment "bindIp" to listen on all request. Add "security" node in your configuration file. My configuration file is in "/etc/mongod.conf".
```
net:
  port: 27017
  #bindIp: 127.0.0.1  # Listen to all request.
security:
  authorization: enabled # be careful there a two space before "authorization"
```
6. restart mongo service
```bash
$ service mongod restart
Stopping mongod:                                           [  OK  ]
Starting mongod:                                           [  OK  ]
```
7. connection mongo with auth, `--authenticationDatabase` is for specifying the database which you create the user. 
```bash
$ mongo localhost:27017/MyDB  -u "user_read" -p "user_read" --authenticationDatabase "admin"
```
show the data we saved in "myCollection"
```bash
> use MyDB
switched to db MyDB
> db.myCollection.find()
{ "_id" : ObjectId("59846a3aba13b68481f3f54a"), "name" : "henryxi" }
```

EOF


