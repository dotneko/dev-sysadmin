# Managing Local Users and Passwords with `NET USER`

- More on the NET services command: [Microsoft XP Documentation: Net services commands](https://www.microsoft.com/resources/documentation/windows/xp/all/proddocs/en-us/net_subcmds.mspx?mfr=true)
- [Net User command for administrators in Windows](http://www.thewindowsclub.com/net-user-command-windows)

```
net user                            # Lists user accounts
net user username                   # Lists info for username
net user username /add              # Adds a user username
net user username /delete           # Deletes a user username
net user username *                 # Prompts for password for username
net user username <new_password>    # Changes the password directly
```
- [TechNet Net User](https://technet.microsoft.com/en-us/library/cc771865(v=ws.11).aspx)

```
net user username * /add                            # Prompts for password
net user username /add /comment:"User Comment"      # Add comment for user
net user username /active:{yes|no}
net user username /homedir:<Path>                   # Does not auto create until you log on
net user username /expires:jan,9,2017               # Set account expiry for username
```

- Note that when remove username, the user directory is not deleted.
- Need to manually delete with `rd` or `rmdir`; `/s` option removes recursively.
- If delete an account and then recreate a new account with the same name, by default a new folder is created (Windows treats them as new and separate accounts).

- For managing local user accounts with Powershell, see: [Managing Local User Accounts with PowerShell](https://mcpmag.com/articles/2015/05/07/local-user-accounts-with-powershell.aspx)

# Managing Local Groups using `NET LOCALGROUP`
```
net localgroup      # Local groups on individual device.
net groups          # Not available unless Active Directory set up (Windows Domain Controller)
net localgroup /?
net localgroup groupname                        # Creates a group named "groupname"
net localgroup groupname username /add          # Adds "username" to the group "groupname"
net localgroup groupname user1,user2 /delete    # Deletes user1 and user2 from "groupname"
```
