# Recovering VirtualBox VHD and Snapshots

Problem: For an unknown reason, my Solaris VM .VHD file got corrupted, and although the .VHD file was able to be loaded into VirtualBox, the snapshots were unusable.

### Exploring Configuration Files
- Assuming the VirtualBox Machine was named "Vbmach", the VM folder is stored in the `Users/VirtualBox VMs/` folder, with a configuration file named `Vbmach.vbox`

### Parent UUID Problems
- Source: https://forums.virtualbox.org/viewtopic.php?f=6&t=79896
- When facing Parent UUID problems, one can use the `vbmanage` command (located in the VirtualBox installation folder):
- Example of an error:
```
Parent UUID {00000000-0000-0000-0000-000000000000} of the medium 'C:\Users\User\VirtualBox VMs\Ubuntu\Snapshots/{e2758629-df3a-4f02-a9a3-eb1cfa43fcaf}.vhd' does not match UUID {eb1dad3e-8223-4284-9534-588b1af20c25} of its parent medium stored in the media registry ('C:\Users\User\.VirtualBox\VirtualBox.xml').
```

First get information on each snapshot (.vhd) and the main .vmd file using:

```
vbox manage internalcommands dumphdinfo harddisk0.vhd
```
After retrieving a dump of of the info in each of the files, I noted that two of the files had a uuidParent={00000000-0000-0000-0000-000000000000}.

Going through the sequential list of .VHD snapshots, the problem identified was that the main .VHD file and the first visible snapshot in the directory that the above invalid uuid, and so could not chain with each other.

The issue was solved by:
1. Setting the main .VHD file's parent UUID equal to the Machine UUID (Found in the .VirtualBox/virtualbox.xml file, or visible in the `Vbmach.vbox` configuration file.
2. Setting the first snapshot with the invalid parent UUID to the UUID of the main.VHD file.

```
vboxmanage.exe internalcommands sethdparentuuid "C:\Path\to\Vbmach.vhd" {<parent-UUID>}
vboxmanage.exe internalcommands sethdparentuuid "C:\Path\to\Snapshots\{<uuid>}.vhd"
```
