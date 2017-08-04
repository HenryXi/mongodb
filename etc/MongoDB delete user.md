# MongoDB delete user
If MongoDB does not enable auth you can delete user without authorisation. If MongoDB enables auth you need to make 
sure you are `userAdmin` or `userAdminAnyDatabase` role before deleting the user. User following command to delete 
the user.
```bash
> use admin
switched to db admin
> db.getUsers()
[
	{
		"_id" : "admin.user_read",
		"user" : "user_read",
		"db" : "admin",
		"roles" : [
			{
				"role" : "read",
				"db" : "MyDB"
			}
		]
	},
	{
		"_id" : "admin.user_read_write",
		"user" : "user_read_write",
		"db" : "admin",
		"roles" : [
			{
				"role" : "readWrite",
				"db" : "MyDB"
			}
		]
	},
]
> db.dropUser("user_read")
true
```

EOF