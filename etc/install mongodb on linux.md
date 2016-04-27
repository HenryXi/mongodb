# Install MongoDB on CentOS
In this page I will show you how to install MongoDB on CentOS. I recommend you install MongoDB by ``yum`` command.
Before installing, you need to add ``/etc/yum.repos.d/mongodb-org-3.0.repo`` file. I install 3.0 version, you can
change this number to install different version, click [here](https://repo.mongodb.org/yum/redhat/) to get which
version are available. Add following code in repository file.
```
[mongodb-org-3.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.0/x86_64/
gpgcheck=0
enabled=1
```
Save this file and type the command
```
sudo yum install -y mongodb-org
```
After all packages download and install type ``mongo`` on your command line. You will see the output like below
```
MongoDB shell version: 3.0.11
connecting to: test
2016-04-27T07:55:31.164+0800 W NETWORK  Failed to connect to 127.0.0.1:27017, reason: errno:111 Connection refused
2016-04-27T07:55:31.166+0800 E QUERY    Error: couldn't connect to server 127.0.0.1:27017 (127.0.0.1), connection attempt failed
    at connect (src/mongo/shell/mongo.js:179:14)
    at (connect):1:6 at src/mongo/shell/mongo.js:179
exception: connect failed
```
Congratulations! You have installed MongoDB successfully.