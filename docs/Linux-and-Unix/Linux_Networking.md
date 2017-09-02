### Basic Commands

```
ifconfig -a
arp -a
```

### Controlling Network Interfaces

Display IP addresses:

```
ip addr show
ip addr show <interface: eth0>
```

Add a new IPv4 address:

```
ip addr add <ip-addr>/<CIDR> dev <device
ip addr add 172.16.1.2/24 dev eth1
```

Remove an IPv4 address:

```
ip addr del <ip-addr>/<CIDR> dev <device>
ip addr del 172.16.1.2/24 dev eth1
```

Bringing an interface up and down:

```
ip link set eth1 down
ip link set eth1 up
```

View basic network statistics:

```
ip -s link
ip -s link ls <interface>   # Specific interface
ip -s -s link ls eth0      # Add -s for additional info
```

### Monitoring Network Connections

Show Connections:

```
ss -t     # TCP Established connections
ss -u     # UDP connections
ss -lt    # Listening TCP ports
ss -ltn   # Listening ports, no hostname lookups (faster)
ss -lun   # Listening UDP ports
ss -ltun  # All listening ports
```

### Basic OS statistics with `sysstat` tools

Installation on Debian-based systems:

```
sudo apt-get install sysstat    # Debian-based distros
sudo yum install sysstat        # RHEL-based distros
```

Gather basic OS statistics:

```
vmstat [delay [count]]
vmstat 1 99   # Reports every 1 second, 99 times.
```

Output key:

- `procs - r`: Total num processes waiting to run
- `procs - b`: Total num busy processes
- `memory - swpd`: Used virtual memory
- `memory - free`: Free virtual memory
- `memory - buff`: memory used as buffers
- `memory - cache`: memory used as cache
- `swap - si`: memory swapped from disk (each second)
- `swap - so`: memory swapped to disk (each second)
- `io - bi`: blocks in (received from device each second)
- `io - bo`: blocks out (sent to device each second)
- `system - in`: interrupts per second
- `system - cs`: context switches
- `cpu - us,sys,id,wa,st`: CPU user time, system time, idle time, wait time.

Show memory usage information (active/inactive):

```
vmstat -a 1 99
```

Reformat output in megabytes:

```
vmstat -a -S M 1 99
```

Gather information for disks/block devices:

```
vmstat -d 1 99
vmstat -d -w     # Wide output
```

Detailed statistics of IO on a server with `iostat`:

```
iostat [delay [count]]
```

Specify device for IO statistics:

```
iostat -d -p sda 1 99
```

### Historical Resource Usage with SAR

- System Activity Report (SAR) tool is included with the `sysstat` tools, and needs to be enabled:

Edit the `/etc/default/sysstat` by changing the `ENABLED="false"` to `ENABLED="true"`, then restart service:

```
sudo service sysstat restart
```

- Data is collected every 10 minutes using a simple cron job configured within `/etc/cron.d/sysstat`

View basic CPU statistics and wait times:

```
sar -u    # Basic CPU statistics and wait times
sar -r    # Available memory statistics
sar -b    # IO stats for individual block devices
```

----

References:

- Duffy, M. (2015). *DevOps Automation Cookbook*. Birmingham: Packt Publishing
