# [Oracle Solaris 11 Roles @ The Urban Penguin](https://www.theurbanpenguin.com/oracle-solaris-11-roles/)

    - RBAC and Roles allow implementation of the least privileged security model.
    - Root user is a role rather than a typical user, so cannot log in directly to the account, but may still use `su`
    - Users cannot use root even if they know the root password; users can only use the root role if it is assigned to them.

- [Oracle Solaris 11 Security Privileges and Authorizations](http://www.oracle.com/technetwork/systems/hands-on-labs/s11-security-1408641.html)

```
rolemod -K roleauth=user root
    # Require users own password when switching to root role.

rolemod -K roleauth=role
    # Require pasword of the role itself.
```

Profiles in Solaris 11 RBAC allow authorizations and privileged commands to be grouped together and can be assigned to users or to roles.

```
profiles -a |more
profiles -p "User Management" info
```

# More on RBAC And Privileges
- [c0t0d0s0.org Tutorial on RBAC](http://www.c0t0d0s0.org/archives/4073-Less-known-Solaris-features-RBAC-and-Privileges-Part-1-Introduction.html)
- [c0t0d0s0.org Using pfexec to delegate administration](http://c0t0d0s0.org/archives/4844-Less-known-Solaris-features-pfexec.html). Very useful article.

    - `pfexec <command>` is a way to execute commands within your rights profile without using su or sudo.
