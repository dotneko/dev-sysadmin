# [Basics of Service Management Facility (SMF) on Oracle Solaris 11](http://www.oracle.com/technetwork/articles/servers-storage-admin/intro-smf-basics-s11-1729181.html)

- A software framework that manages the services on a system.
- Each service has a well-defined state and a relationship to other dependent services.
- Ability to run multiple instances of a given service and share common configuration.
- Configuration repository managed by `svc.configd`
- Each service described using a Fault Management Reousrce Indicator (FMRI)
- SMF framework always active on Oracle Solaris 11 - started and restarted through the default init process.

---
## Listing services
```
svcs
svcs -a         # Lists additional new service instances.
svcs *ftp*      # Searches for services containing *ftp*
```

## Managing services

If change configuration file, need to restart service using `svcadm` `enable`/`disable`:
```
svcadm disable ftp
svcadm enable ftp
svcadm restart ftp
```
- Note that `svcsadm restart` [does not commit property changes to the running snapshot and does not run the refesh method of the instance](https://docs.oracle.com/cd/E36784_01/html/E36820/svcrestart.html).

# Troubleshooting system services
- [Oracle Solaris 11.2: How to repair an instance that is in maintenance](https://docs.oracle.com/cd/E36784_01/html/E36820/ecdps.html#SVSVFmaintenanceadm)
```
svcs -xv svc:/network/ftp:default       # Troubleshoot the FTP server
```
