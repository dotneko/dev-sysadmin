# NTFS Permissions in WS 2012

- Permissions can be set at both the folder and file level:
    - Full control: can add, change, move, delete and *change permissions*
    - Modify: combination of Read and Write; delete files within folder
    - Read & Execute
    - List folder contents (applies only to folder): does not allow direct read.
    - Read
    - Write: can create files and folders but *cannot read existing information*.

- Note that NTFS permissions assigned are *cumulative*.
- Deny permissions always override Allow permissions.
    - Useful when group permissions have been applied to a folder, but want a user in that group to be denied access to the folder.

- More details from source: [Setting basic NTFS permissions](http://www.techrepublic.com/blog/data-center/setting-basic-ntfs-permissions-in-windows-server-2012/)

- [NTFS Permission Precedence](http://www.ntfs.com/ntfs-permissions-precedence.htm)

    - A general hierarchy of precedence:

        - Explicit Deny
        - Explicit Allow
        - Inherited Deny
        - Inherited Allow

- [Files and Folder Basic NTFS Permissions Table](http://www.ntfs.com/ntfs-permissions-file-folder.htm)

# Permission of shares

    - Full Control – it allows reading, writing, changing, and deleting of any file and subfolder.
    - Change – it is the equivalent of the Modify permission level.
     Read – it is the equivalent of the Read & execute permission level.

- Source: [Windows Network Sharing](http://www.howtogeek.com/school/windows-network-sharing/lesson1/all/)

# What happens when combining share and NTFS permissions?

- Share vs NTFS permissions: The *most restrictive permission* wins out.
    - E.g. Folder - Share: Read-Only for Everyone group
                    NTFS:  Full Control for Everyone group
                => Share permission will mean users are unable to make changes.

- Share permissions are only enforced *if the contents of the shared folder are accessed over the network.*
    - This means that on local server only NTFS permissions will apply

- NTFS vs NTFS permissions are *additive*
    - User A has read rights
    - User A belongs to group that has modify rights
    => User A will have read & modify rights.

>> For many administrators, it's considered a best practice to provide Full Control/Read & Write permissions to shares and then use NTFS permissions to further restrict access if necessary. So, you would simply grant a user or group full share permissions, which would not restrict any access. However, if you wanted to allow only Read rights on the items in the shared folder, you would use NTFS permissions and grant just Read rights.  In this way, regardless of how the folder is accessed - over the network or directly from the server - the same permission set will always apply and it simplifies the permissions game for administrators by basically eliminating one set of permissions that you need to worry about.

- Source: [Tips for setting share vs NTFS permissions](http://www.techrepublic.com/blog/data-center/windows-server-2012-tips-for-setting-share-vs-ntfs-permissions/)

# Changing NTFS Folder Permissions

```
icacls
icacls dirname              # Displays ACL for dirname
icacls dirname /t           # Recursively lists ACLs
icacls dirname /grant:
```
- Source: [NTFS folder permissions with PowerShell](http://tomandersonpro.net/ntfs-permissions-with-powershell/)

# References
- [What is windows "Interactive" User](http://serverfault.com/questions/188115/what-is-windows-interactive-user)
- [WS2008 Managing Permissions for Shared Folders](https://technet.microsoft.com/en-us/library/cc753731(v=ws.11).aspx)
