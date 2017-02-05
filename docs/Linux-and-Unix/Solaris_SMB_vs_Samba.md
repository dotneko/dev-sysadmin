# References

- [Oracle Solaris: SMB Shares](https://docs.oracle.com/cd/E23824_01/html/821-1449/smbshares.html#scrolltoc)


# SMB Server
- Source: [Oracle Solaris Administration: SMB Server](https://docs.oracle.com/cd/E23824_01/html/821-1449/smbenvironmentoverview.html#scrolltoc)
- Oracle 11 allows the Solaris server to be an active participant in a Windows active directory domain.
- SMB server allows serving of files by means of **SMB shares**.
- SMB server can operate in workgroup mode or domain mode:
    - Workgroup mode: SMB server responsible for authentication "local login".
    - Domain mode: User authentication delegated to the domain controller.
- Solaris manages user identities using UIDs/GIDs and Windows SIDs through the `idmap` identity mapping service.
- Note that *Samba and SMB servers cannot be used simultaneously on a single Oracle Solaris system.*

*Difference between Samba and SMB?*

> CIFS and SMB are Windows file sharing protocols. CIFS being the latest version of SMB.
NFS is traditionally a Unix file sharing protocol but now Windows Server supports it natively (the old version anyway--see below).
SMB/CIFS uses Windows-style access control lists (which are really complicated) whereas NFS uses Unix-style file permissions (User ID owner, Group ID owner, and read/write/execute permissions).
On Unix/Linux systems you can use Samba to both share and access filesystems via SMB/CIFS. Samba does a lot more than that though... It can actually act as a drop-in replacement for Microsoft's Active Directory. Linux has built-in support for CIFS shares now so Samba isn't needed in most cases.

- Source: [reddit post by riskable](https://www.reddit.com/r/homelab/comments/2fawvq/eli5_what_is_the_difference_between_smb_cifs_and/)
