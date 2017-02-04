# Role Based Access Control (RBAC) and Administrative Privileges

- Used to control user access to tasks that would normally be restricted to the root role.
- Usage driven by the need for privilege delegation and separation of duties.
- Concepts include roles, rights profiles, authorizations, privileges, and security attributes.
- Process rights management is implemented through privileges.
- Various superuser capabilities are collected into a *rights profile*.
- Rights profiles are assigned to special user accounts, called *roles*.
- One can base roles on rights profiles that have the smae name (e.g. root).

### [Oracle Solaris 11 Roles @ The Urban Penguin](https://www.theurbanpenguin.com/oracle-solaris-11-roles/)

  - RBAC and Roles allow implementation of the least privileged security model.
  - Root user is a role rather than a typical user, so cannot log in directly to the account, but may still use `su`
  - Users cannot use root even if they know the root password; users can only use the root role if it is assigned to them.

### The Root Role

- Initial user account that was created during installation is assigned the root role.

- `roles [username]`
- `usermod -R +root [username]` will assign privileges of the root role to [username] and enable them to assume the root role.

### Adding to sudoers file
- `sudo visudo` or run `visudo` as root
- Add `username ALL=(ALL) ALL` to the file

### Creating a Role
-  `roleadd -D` displays the default settings for a new role or user.
-  `roleadd -A` creates the role and assigns authorizations.
-  `auths username` used to verify role.
-  `roles username` verifies role assignment.

```
roleadd -m -P "User Management" usermx
    # -m: specifies make directories (just like that used in useradd -m)
    # -P: specifies profile "User Management"
    # -A: specifies authorization
    # usermx: the name of the role to be created.
```
- [Oracle Solaris 11 Security Privileges and Authorizations](http://www.oracle.com/technetwork/systems/hands-on-labs/s11-security-1408641.html)

```
rolemod -K roleauth=user root       # Require users own password when switching to root role.
rolemod -K roleauth=role            # Require pasword of the role itself.
```

# Solaris Profiles
Profiles in Solaris 11 RBAC allow authorizations and privileged commands to be grouped together and can be assigned to users or to roles.

In order to find out more about the profiles available, you could use the command:
```
profiles -a|more
```

To find out more about the specific profile such as "User Management" including the authorizations and the commands the profile allows, you could use the command:

```
profiles -p "User Management" info
```
- **Profile shell**

  - In Solaris 11, users and roles can also run privileged applications from a *profile shell*.
  - A special shell that recognizes the security attributes included in a rights profile.
  - Can be assigned to a specific user as a login shell, or started by using the `su` command.
  - In Solaris 11, every shell has a profile shell counterpart (e.g. bash and pfbash).

# More on RBAC And Privileges
- [c0t0d0s0.org Tutorial on RBAC](http://www.c0t0d0s0.org/archives/4073-Less-known-Solaris-features-RBAC-and-Privileges-Part-1-Introduction.html)
- [c0t0d0s0.org Using pfexec to delegate administration](http://c0t0d0s0.org/archives/4844-Less-known-Solaris-features-pfexec.html). Very useful article.

    - `pfexec <command>` is a way to execute commands within your rights profile without using su or sudo.

- [Solaris 11.3 User Rights Management](http://docs.oracle.com/cd/E53394_01/html/E54830/rbac-1.html#scrolltoc)
- [Oracle User Authorizations, Rights Profiles and Roles](http://docs.oracle.com/cd/E53394_01/html/E54830/prbac-moreabt-1.html#OSSUPprbac-25)
