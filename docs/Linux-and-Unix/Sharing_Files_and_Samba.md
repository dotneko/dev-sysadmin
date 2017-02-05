# Legacy Sharing
```
share                       # Display shares (more info than -A ?)
share -A                    # Displays published shares
share -F nfs -o ro ./share  # Defines and publishes a file system share (NFS)
share -F smb -o rw ./share2 # Defines and publishes a file system share (SMB)
unshare share_name          # Unpublishes a share
unshare -a                  # Unpublishes all active shares.
```

# Using the Samba Suite
- In Solaris 11.3, the Samba suite has to be downloaded separately:

```
pfexec pkg install samba    # or run as root
```

- No configuration file exists on installation, but an example configuration file `smb.conf-example` exists in the `/etc/samba` directory.
- Can create new config file or use the `smb.conf-example` as a template -> the samba service will look for the configuration file at `/etc/samba/smb.conf`
- Can examine the default share named `[homes]` under the share definitions.

### Create a user for samba
```
useradd samba
passwd -r files samba           # -r files option specifies password for file system.

smbadm enable-user samba        # Enables samba service for user samba.
```

# Miscellaneous
- Accessing a Solaris file share from Windows Command Line
```
net use x:\\<ipaddress>
```
- `dfshares`: Lists information about resources available to the host through a distributed file system.
