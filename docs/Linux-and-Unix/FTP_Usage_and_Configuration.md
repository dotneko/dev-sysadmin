# File Transfer Protocol (FTP)

- An old file transfer protocol for exchanging files over a TCP/IP network since the 1970's.
- Base specification is [RFC 959](http://www.ncftp.com/ncftp/rfc959.html), 1985.
- Designed to allow clients to browse the file system, and FTP is a stateful sequence of one or more transactions.
- Client is always responsible for initiating requests.
- Authentication by username/password; de facto standard for guest access using "anonymous" for username and an "email address" for the password.
- Supports **ASCII** for text and "image" for binary data.
- *Base specification does not have any special handling for encrypted communications, so files containing sensitive material should not be sent.*
- **Usernames and passwords are sent in clear text** and the entire FTP transmission could be monitored by potential attackers.
- Instead should instead use something like `scp` for same security as `ssh`.

*Source:* [http://www.ncftp.com/libncftp/doc/ftp_overview.html](http://www.ncftp.com/libncftp/doc/ftp_overview.html)


# FTP service on Solaris

```
svcs ftp                # Check status of ftp service (default: disabled)
svcadm enable ftp       # Enables FTP
svcs -xv svc:/network/ftp:default       # Run for troubleshooting
```

# Basic FTP Usage

```
ftp
ftp -i                  # Opens FTP and turns off interactive mode so mget/mput
                        # will not ask for confirmation.
```

# Basic FTP commands

```
ftp> help
ftp> open 192.168.40.153
ftp> put filename.txt   # Transfer single file
```

## Local

```
ftp> lcd            # Lists local directory, or changes local directory
ftp> !ls            # Lists files in local directory - doesn't work with default Windows cmd.exe FTP
ftp> !dir           # Lists files in local directory - works with MS FTP
```

## Remote

```
ftp> get            # Retrieves files
ftp> mget           # Retrieves multiple files
ftp> put            # Sends one file
ftp> mput           # Sends multiple files; note that directories are not transferred automatically (see bottom of page).
```
# Configuring ProFTPD.conf
- Detailed configuration documentation at [proftpd.org](http://www.proftpd.org/docs/howto/ConfigFile.html)
- Configuration is done through editing the `/etc/proftpd.conf` file.
- The file `/etc/ftpd/ftpusers` in Solaris contains a list of users denied access to the FTP server, e.g. root.
- See [Oracle: Controlling FTP Server Access](https://docs.oracle.com/cd/E23823_01/html/816-4555/wuftp-43.html) for more information.
- Note that any change of the file requires restarting the ftp service.
    - Solaris: `svcadm restart ftp`

## Changing the FTP Connection Message
- Configured under `DisplayConnect` in `/etc/proftpd.conf`.
- By default `DisplayConnect` is configured to display the contents of the `/etc/issue` text file.

```
DisplayConnect      /etc/issue
```

- One can modify this to point to another file or edit the `/etc/issue` file directly.

## Confine FTP users to their home directory
In `/etc/proftpd.conf`, example:
```
DefaultRoot         ~       # Causes every FTP user to be "jailed" into their home directory.
```

## Changing the FTP Closing Message
In `/etc/proftpd.conf`, example, can point the message to /etc/quitmessage
```
DisplayQuit         /etc/quitmessage
```

## Controlling who can connect through FTP
- Using the following directive would deny all access by default:
```
<Limit LOGIN>
DenyAll
</Limit>
```
- The above would be used if one wants to allow access to specific users, e.g. Anonymous., where you would add the following within the  <Anonmyous ~ftp> section:
```
<Anonymous ~ftp>
    <Limit LOGIN>
        AllowAll
    </Limit> ....
</Anonymous>
```

## Configuring anonymous FTP (No write access)
- By default, Solaris 11 does not allow for anonymous connections.
- To enable, one can add the following according to [www.proftpd.org](http://www.proftpd.org/docs/configs/basic.conf):
- Also need to make sure `ftp` is removed from the ftp deny list that is stored in `/etc/ftpd/ftpusers` (Solaris).
```
# A basic anonymous configuration, no upload directories:
<Anonymous ~ftp>
  User				ftp
  Group				ftp

  # We want clients to be able to login with "anonymous" as well as "ftp"
  UserAlias			anonymous ftp

  # Limit the maximum number of anonymous logins
  MaxClients			10

  # We want 'welcome.msg' displayed at login, and '.message' displayed
  # in each newly chdired directory.
  DisplayLogin			welcome.msg
  DisplayFirstChdir		.message

  # Limit WRITE everywhere in the anonymous chroot
  <Limit WRITE>
    DenyAll
  </Limit>
</Anonymous>
```

## Configuring anonymous FTP (with an upload directory)

- Add the following within the <Anonymous></Anonymous> section from above:
```
# An upload directory that allows storing files but not retrieving
# or creating directories.
<Directory uploads/*>
  <Limit READ>
    DenyAll
  </Limit>

  <Limit STOR>
    AllowAll
  </Limit>
</Directory>
```
- For detailed example configuration, see example:  [anonymous.conf](http://www.proftpd.org/docs/configs/anonymous.conf)

## Transferring directories
- FTP will not automatically create and transfer directories when using `mput`.
- It would be better to use `scp` for better security and support for recursive transfer of files/subdirectories.
- Anyway here's a bash script that could recursively transfer directories with their contents through FTP...*currently only runs on Bash for Windows with MS FTP.*

```
if [[ "$1" = "help" ]]; then
  echo "Run with ftpcdir.sh <directory> <host address> <username> <password>"
  exit
fi
find $1 -type d > dirs.txt
find $1 > files.txt
echo open $2 > command.ftp
echo $3 >> command.ftp
echo $4 >> command.ftp
for i in `cat dirs.txt`
do
  if [[ "$i" != '.' ]]; then
    echo mkdir $i >> command.ftp
  fi
done
for i in `cat files.txt`
do
  if [[ "$i" != '.' ]]; then
    echo put $i $i >> command.ftp
  fi
done
echo quit >> command.ftp
ftp -s:command.ftp                  # Only works with Windows Cmd FTP
exit
```
