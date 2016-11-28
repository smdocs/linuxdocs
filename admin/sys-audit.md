#Linux System Audit

####Two most important questions for a Linux production system 
1. How many unique outbound TCP connections have your servers made in the past hour?
2. Which processes and users initiated each of those connections?

Collect syscalls as a source of data for continuous monitoring of the system.

[Linux Audit](https://people.redhat.com/sgrubb/audit/) has been part of the kernel since 2.6.(14?). 
  - The audit system consists of two major components. The first component is some kernel code to hook and monitor syscalls. 
  - The second bit is a userspace daemon to log these syscall events.
  
Let's say we want tp log an event whenever someone reads a specific file. With auditd, we must first tell the kernel 
that we want to know about these events. We accomplish this by running the userspace auditctl command as root with the 
following syntax:
```bash
$ auditctl -w /data/topsecret.data -p rwxa

```
Now, every time ```/data/topsecret.data``` is accessed (regardless of whether it was via symlink), the kernel will generate 
an event. The event is sent to a userspace process (usually auditd) via something called a “netlink” socket. 
(The tl;dr on netlink is that you tell the kernel to send messages to a process via its PID, and the events appear on this socket.)

Userspace auditd process then writes the data to ```/var/log/audit/audit.log```. If there is no userspace process connected 
to the netlink socket, these messages generally appear on the console and can be seen in the output of dmesg.

Daemon processes (or rogue netcats, ahem) usually use the listen syscall to listen for incoming connections. For example, 
if Apache wants to listen for incoming connections on port 80, it requests this from the kernel. To log these events, we again 
notify the kernel of our interest by running auditctl:

```bash
 $ auditctl -a exit,always -S listen
```
Now, every time a process starts listening on a socket, we receive a log event. This logging can be applied to any syscall you like.

In order to answer question 1, i.e. How How many unique outbound TCP connections have your servers made in the past hour?  
we will  nned to monitor the ```connect``` system call. If we want to watch every new process or command on a host, 
check out execve.

[go-audit](https://github.com/slackhq/go-audit)
[](https://slack.engineering/syscall-auditing-at-scale-e6a3ca8ac1b8#.9pq1ww1qm)
