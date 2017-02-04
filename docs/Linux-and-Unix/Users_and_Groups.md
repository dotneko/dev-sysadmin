# Users and User Accounts

- All users are assigned a **UID**. Maximum number for UID or GID is 2 to the power of 31 (2147483647)
- Users are generally **standard users**:

    - Considered "interactive" - can log into the system locally or remotely.
    - Will have a home directory associated with it, can be located either on local system or remote file server.
    - Groups can be assigned based on user type, location, shared files/directories.

- Special 'users' include the "super user" root and special accounts, and have **special UIDs**:

    - UID 0-99: reserved for Oracle Solaris system
    - UID 0: root
    - UID 1: daemon
    - UID 2: bin pseudouser
    - UID 60001 and 65534: reserved for nobody and nobody4 (NFS Anonymous users)
    - UID 60002: noaccess

### System Accounts

- Associated with an application process that is installed and running on the system.

  - An application process that listens on a network port for service requests is referred to as a **daemon**.

- These running processes need a way to operate on the system just as standard users do.
- System account usually does not require a home directory.
- Provides a basic level of security to the system by protecting it in the event that the service that the service associated  with the account is violated.

### Root Account

- Called "super user" in previous Solaris releases - owner of most binaries and configuration files.
- Root account in Oracle Solaris 11 is generally configured as an RBAC role.

  - This means it cannot be logged in directly and users must be explicitly granted to access to the account.
  - When you're authenticating to a role, the password must be that of the role.

- If given the root role/access, one can assume the role using `su`.
- If want `sudo` access, need to edit the `/etc/sudoers` file for the user ([Source](https://blogs.oracle.com/observatory/entry/sudo)):

```
user_name ALL=(ALL) ALL
```
- In Solaris, commands authorized the user's assigned role can be executed with `pfexec`
- Why one should use `pfexec` instead of `sudo`: [Link](https://lildude.co.uk/solaris-11-express-root-password-gotcha)

### Examining Users
```
whoami              # Who the current user is
who                 # Who is logged on to the system
getent passwd       # Examines system's list of users
finger              # Displays who is logged on to the system (like who)
finger user_name    # Displays information about the user user_name
```

### Adding, Changing, Deleting Users
```
useradd -m username
useradd -m username	        # simple way to create a new user with username
useradd -c "Common name" -d [home directory, e.g. /export/home/username] -m username
useradd -c "User1" -d -m -u:101 -g:staff User1
```
N.B. Very important to use -m for make, otherwise directory will not be created
```
usermod -c
usermod -u [userid]
usermod -d
```
To delete a user:
```
userdel username          # Preserves user's home directory.
userdel -r username       # Removes user's home directory.
```
If wanting to delete a user's home directory that was not deleted before, the user folder must be unmounted before it could be deleted.
```
umount dirname
```

### Password information
```
passwd username
```
- In `/etc/shadow` file stores passwords when using /etc files
- In `/etc/passwd` file when using NIS
- In `people` container when using LDAP

- Default password requirements stored in `/etc/default/passwd` file

## Standard Users

- Interactive in the sense that user can log into the system locally or remotely.
- Will have a home directory associated with it, can be located either on local system or remote file server.

## System Accounts

- Associated with an application process that is installed and running on the system.

  - An application process that listens on a network port for service requests is referred to as a **daemon**.

- These running processes need a way to operate on the system just as standard users do.
- System account usually does not require a home directory.
- Provides a basic level of security to the system by protecting it in the event that the service that the service associated  with the account is violated.

## Root Account

- Called "super user" in previous Solaris releases - owner of most binaries and configuration files.
- Root account in Oracle Solaris 11 is generally configured as an RBAC role.

  - This means it cannot be logged in directly and users must be explicitly granted to access to the account.
  - When you're authenticating to a role, the password must be that of the role.

- Given the root role, one can assume the role using `su`
- If want `sudo` access, need to edit the `/etc/sudoers` file for the user ([Source](https://blogs.oracle.com/observatory/entry/sudo)):

```
user_name ALL=(ALL) ALL
```
- In Solaris, commands authorized the user's assigned role can be executed with `pfexec`
- Why one should use `pfexec` instead of `sudo`: [Link](https://lildude.co.uk/solaris-11-express-root-password-gotcha)

# UNIX Groups
- Each group has a name, group ID (GID), and a list of usernames that belong to the group.
- Two types of groups:
    - **Primary group:** group that OS assigns files that are created by the user.
    - **Secondary group:** other groups a user belongs to, maximum 1024 supplemental groups.

To display the list of groups for the user:
```
groups username
```
List groups
```
getent group
```
List users in a group
```
getent group groupname
```

## Adding and modifying groups
```
groupadd -U user1[,user2]
groupmod
groupdel

useradd -g group-primary
useradd -G group-secondary
getent group
usermod -g group-primary username
usermod -G +group1,group2... username
usermod -G -group2,group3... username
usermod -G "" username    # removes all secondary groups
```

# Links and References:
- [Oracle Solaris 11.3 Information Library](https://docs.oracle.com/cd/E53394_01/)
