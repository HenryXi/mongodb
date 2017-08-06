# MongoDB Authentication Mechanisms
When you connect MongoDB with auth you need to specify the "Authentication Mechanisms". If your MongoDB version 
is 3.0+ the default "Authentication Mechanisms" is **SCRAM-SHA-1**, for other versions **MONGODB-CR** as the default.

**db.auth()**

The `db.auth()` method with mechanisms example:
```bash
db.auth( {
   user: <username>,
   pwd: <password>,
   mechanism: <authentication mechanism>
} )
```

**command line** (`SCRAM-SHA-1` as default)

```bash
mongo host:port/<database_name>  -u "<user_name>" -p "<user_pwd>" --authenticationDatabase "<auth_db>" --authenticationMechanism "SCRAM-SHA-1"
```