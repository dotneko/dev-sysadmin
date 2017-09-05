Vagrant
=======

- [Vagrant Docs](https://www.vagrantup.com/docs/index.html)

### Starting and stopping VMs

```
vagrant init
vagrant up
vagrant halt
```
Connecting to the VM:

```
vagrant ssh
```

Restarting the VM:

```
vagrant reload
```

### Check Guest OS Sates

```
vagrant status
```

### Suspending/Resuming

Suspend (saves snapshot) with:

```
vagrant suspend
```

Resume with:

```
vagrant up
vagrant resume
```

### Removing VMs

```
vagrant global-status
vagrant destroy <ID>
```

To remove stale VMs:

```
vagrant global-status --prune
```

### Using Vagrant with Version Control

- `Vagrantfile` should be in version control.
- `.vagrant/` should be ignored by version control: add to `.gitignore`

# Managing Boxes

List installed boxes:

```
vagrant box list
```

Remove an installed box:

```
vagrant box remove <name>
```
