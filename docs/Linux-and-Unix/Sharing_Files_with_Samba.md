# Using the Samba Suite
- In Solaris 11.3, the Samba suite has to be downloaded separately:

```
pfexec pkg install samba    # or run as root (may need to --accept license)
```


### Configuring Samba: `/etc/samba/smb.conf`
- No configuration file exists on installation, but an example configuration file `smb.conf-example` exists in the `/etc/samba` directory.
- One can use the existing `/etc/samba/smb.conf-example` as a template, copy it `/etc/samba/smb.conf` and make the necessary modifications (need set w permission)
- `smb.conf` has 2 sections: global settings, share definitions.

    - Workgroup name should be changed.
    - Confirm authentication is set to user `security = user`

- Share definitions
    - `[home]` defines default share access to home folders.
- Example share definition
```
[smbdemo]
    comment = Samba Share
    path = /smbdemo
    browsable = yes
    guest ok = yes
    read only = no
    create mask = 0755
```
### Creating a new directory for sharing using Samba
```
mkdir /smbdemo
chmod 770 /smbdemo
```

### Create a users and groups for Samba
```
useradd samba           # Optional, but user for samba must be an existing user.
smbpasswd -a <username>
```

### Creating the Samba group
```
groupadd smbusers
chown :smbusers /smbdemo
usermod -G smbusers <username>
```

### Enabling Samba
```
svcadm disable samba
svcadm enable samba
smbadm enable-user samba        # Enables SMB service for user samba.
testparm                        # Tests configuration
```
- N.B. Using the above configuration works for sharing files without using legacy sharing commands like share/unshare for configuration.

# Legacy Sharing Commands
```
share                       # Display shares (more info than -A ?)
share -A                    # Displays published shares
share -F nfs -o ro ./share  # Defines and publishes a file system share (NFS)
share -F smb -o rw ./share2 # Defines and publishes a file system share (SMB)
unshare share_name          # Unpublishes a share
unshare -a                  # Unpublishes all active shares.
dfshares                    # Lists information about resources available to the host through a distributed file system.
```

# Miscellaneous
- Accessing a Solaris file share from Windows Command Line
```
net use x:\\<ipaddress>
```
- Accessing the SMB file share: `smb://<ip address>`

# References
- [Creating network share via Samba via CLI Linux Terminal](https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20(Command-line%20interface/Linux%20Terminal)%20-%20Uncomplicated,%20Simple%20and%20Brief%20Way!)
- [Linux File Server Step-by-step config guide](http://www.tomsitpro.com/articles/linux-server-configuration-guide-book-excerpt,2-777-2.html)
