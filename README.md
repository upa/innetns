
# innetns: a simple script to run commands in network namespaces

This script helps you to run commands in network namespaces simply.

Usage:

```
$ innetns
usage: innetns [-h] [-l] [-s] [netns] [command ...]

netnsin: execute command in netns

positional arguments:
  netns          string to identify a network namespace
  command        command to execute in netns (default is `su [USER]`)

options:
  -h, --help     show this help message and exit
  -l, --list     list network namespaces
  -s, --wo-sudo  call `ip netns exec` without sudo
```

Examples:

* List network namespaces

```
$ innetns -l 
NOC_v1003
NOC_v1004
NOC_v1005
```

* Enter a network namespace

```
$ innetns 1003
[sudo] password for upa: 
$
# Now the shell is in network namespace NOC_v1003
```

* Run commands in a network namespace

```
$ innetns 2003 ping 1.1.1.1 -c 3
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=55 time=4.59 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=55 time=4.55 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=55 time=5.00 ms

--- 1.1.1.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 4.553/4.712/4.998/0.202 ms
```

* When `[netns]` argument cannot deteremine a single traget netns, it
  lists candidate namespaces.

```
$ innetns NOC
There are multiple candidates:
NOC_v1003
NOC_v1004
NOC_v1005
```


Install:

```
git clone https://github.com/upa/inetns
cd inetns && sudo make install
```
