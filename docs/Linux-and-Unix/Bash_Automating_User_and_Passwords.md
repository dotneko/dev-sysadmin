# Simple Example (Solaris)

***Task: Automate creation of users with a default password via a bash script***

- List of users are included in a `users.txt` containing usernames:

```
User1
User2
User3
User4
Test1
Test2
Test3
Test4
```

- Since the `passwd` command in Solaris does not have an `-stdin` option for standard input, an **expect script** needs to be created, which takes an argument for the username to create a password.
- The password in this example = username+123, i.e. User1's password is User1123
- For example, `userpass.exp`:

```
#!/bin/expect
set tag 123
set password $argv$tag
spawn passwd $argv
expect "Password:"
send "$password\r";
expect "Password:"
send "$password\r";
interact
```

- Now a bash script could be created to create a new user account and run the expect script to create a default password.
- For example, `user-pass.sh`:

```
#!/bin/bash
for i in $(cat users.txt)
do
  useradd -m $i             # Creates a user
  ./userpass.exp $i         # Runs the expect script to add the password
done
exit
```
- To run, execute `./users-pass.sh` as root.

# More Complex Example (Solaris)

***Task: To automatically create user accounts from a text file with additional information.***

- N.B. [Scripts below pushed to github repository](https://github.com/gavchan/sol-scripts)
- E.g. `userslist.txt` file contains usernames and passwords, first and last names:

```
user1 password1 User1 Last1
user2 password2 User2 Last2
user3 password3 User3 Last3
user4 password4 User4 Last4
test1 password1 Test1 Last1
test2 password2 Test2 Last2
test3 password3 Test3 Last3
test4 password4 Test4 Last4
```

A simple expect script `userpass.exp` to enter <argv> as password:

```
#!/bin/expect
set username [lindex $argv 0]
set password [lindex $argv 1]
spawn passwd $username
set sp_id $spawn_id
expect "Password:"
send "$password\r";
expect "Password:"
send "$password\r";
wait $spawn_id
close
```
- N.B. For some reason closing with `interact` didn't work like the first script, so instead used `wait` to allow the `passwd` process to finish, then `close`.

A bash script to read the `userslist.txt` file and create users with necessary info, `create-users.sh`:

```
#!/bin/bash
echo "Creating users from file userslist.txt"
while IFS=" " read col1 col2 col3 col4
do
  echo "Creating account $col1 for $col3 $col4".
  useradd -m -c "$col3 $col4" $col1
  echo "Password for username $col1 is: $col2"
  ./userpass.exp $col1 $col2
done < userlist.txt
exit
```

# References:
- [How to parse a CSV file in Bash](http://stackoverflow.com/questions/4286469/how-to-parse-a-csv-file-in-bash)
