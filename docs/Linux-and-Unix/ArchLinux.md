- [ArchLinux Wiki](https://wiki.archlinux.org/)

### Installation
- [ArchLinux Installation](https://wiki.archlinux.org/index.php/Installation_guide)
- [Installing ArchLinux in VirtualBox](https://uvesway.wordpress.com/2015/03/11/how-to-install-arch-linux-on-a-vm-virtualbox/) (Worked well with minor adjustments)

### Mounting an additional internal drive at boot
- Edit fstab: [Accessing an internal drive](http://www.linuxquestions.org/questions/linux-newbie-8/arch-linux-how-to-get-access-to-my-internal-hard-drive-can%27t-change-permissions-4175592413/)
```
/dev/sdc4 /media/anyname rw,auto,user 0 0
```

### Installing files from the ArchLinux User Repository
- [ArchLinux installing "AUR" packages](https://wiki.archlinux.org/index.php/Help:Reading#Installation_of_packages)

### Deluge
- [ArchLinux Wiki: Deluge](https://wiki.archlinux.org/index.php/Deluge)

*Installation Notes*

- "Import Error: No module named gtk" when running `deluge-gtk`: install `pygtk` package.

### Network Manager

- [Network Manager with Gnome3](https://evilshit.wordpress.com/2012/09/15/how-to-make-networkmanager-and-network-manager-applet-work-on-arch-linux-with-gnome3/)
- [ArchLinux Wiki Network Manager](https://wiki.archlinux.org/index.php/NetworkManager)

### PIA
- Finally got it working via NetworkManager/OpenVPN using [PIA's script](https://www.privateinternetaccess.com/pages/client-support/ubuntu-openvpn)

### Redshift (F.lux alternative for Linux)
- [Redshift Project Web Page](http://jonls.dk/redshift/)
- [Redshift Archlinux Page](https://wiki.archlinux.org/index.php/Redshift)

*Installation Notes*

- Installation with `pacman -S redshift` worked fine.
- Noted when trying to run `redshift-gtk1` needed to install `python-gobject` and `python-xdg` as noted on the ArchLinux Wiki.
- Install as service: `systemctl enable /usr/lib/systemd/redshift-gtk.service`
- Manually configure `~/.config/redshift.conf` file.
