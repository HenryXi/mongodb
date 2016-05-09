# Install MongoDB as windows service
In this page I will show you how to install MongoDB in windows as service. Download MongoDB .msi file
[here](https://www.mongodb.org/downloads) and install. I assume that you install it in ``C:\Program Files\MongoDB``.
MongoDB will connect ``C:/data/db`` as default dbpath, if this directory doesn't exist you have to tell
MongoDB the right dbpath. I create two directories for log(``D:\mongo_data\log``) and database(``D:\mongo_data\db``).

**Start MongoDB Service**
Before configuring MongoDB service you have to use following command to start MongoDB service. 
```
cd C:\Program Files\MongoDB\Server\3.0\bin 
mongo.exe --dbpath D:\mongo_data\db
```

You will see the output like following 
```
2016-05-05T18:16:24.754+0800 I CONTROL  Hotfix KB2731284 or later update is not installed, will zero-out data files
2016-05-05T18:16:24.755+0800 I CONTROL  [initandlisten] MongoDB starting : pid=4772 port=27017 dbpath=D:\mongo_data\db 64-bit host=yong-PC
2016-05-05T18:16:24.755+0800 I CONTROL  [initandlisten] targetMinOS: Windows Server 2003 SP2
2016-05-05T18:16:24.755+0800 I CONTROL  [initandlisten] db version v3.0.10
2016-05-05T18:16:24.755+0800 I CONTROL  [initandlisten] git version: 1e0512f8453d103987f5fbfb87b71e9a131c2a60
2016-05-05T18:16:24.756+0800 I CONTROL  [initandlisten] build info: windows sys.getwindowsversion(major=6, minor=1, build=7601, platform=2, service_pack='Service Pack 1
2016-05-05T18:16:24.756+0800 I CONTROL  [initandlisten] allocator: tcmalloc
2016-05-05T18:16:24.756+0800 I CONTROL  [initandlisten] options: { storage: { dbPath: "D:\mongo_data\db" } }
2016-05-05T18:16:24.766+0800 I JOURNAL  [initandlisten] journal dir=D:\mongo_data\db\journal
2016-05-05T18:16:24.766+0800 I JOURNAL  [initandlisten] recover : no journal files present, no recovery needed
2016-05-05T18:16:24.777+0800 I JOURNAL  [durability] Durability thread started
2016-05-05T18:16:24.778+0800 I JOURNAL  [journal writer] Journal writer thread started
2016-05-05T18:16:24.785+0800 I NETWORK  [initandlisten] waiting for connections on port 27017
```
You can press ``Ctrl + c`` to stop the service. As you can see it is a tedious process to start and stop the service.
Next, I will show you how to configure MongoDB as windows service.

**Configure MongoDB Service**

Create a configuration file at ``C:\Program Files\MongoDB\Server\3.0\mongod.cfg`` like following.
```
systemLog:
    destination: file
    path: D:\mongo_data\log\mongod.log
storage:
    dbPath: D:\mongo_data\db
```
Open windows command line and change directory to MongoDB installed and install MongoDB as windows Service
```
cd C:\Program Files\MongoDB\Server\3.0\bin
mongod.exe --config "C:\Program Files\MongoDB\Server\3.0\mongod.cfg" --install
```
After executing the commends you can find MongoDB service in Windows Service Management(Win + R --> 
services.msc --> Enter)

You can create a shortcut to quick start and stop MongoDB service. How to create shortcut? Click [here](http://www.henryxi.com/quick-launch-programsstart-service-on-windows).