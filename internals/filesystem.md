#Linux File System ```/proc```

```/proc/1```
- A directory with information about process number 1. Each process has a directory below /proc with the name being its process identification number.

```/proc/cpuinfo```
- Information about the processor, such as its type, make, model, and performance.

/proc/devices
List of device drivers configured into the currently running kernel.

/proc/dma
Shows which DMA channels are being used at the moment.

/proc/filesystems
Filesystems configured into the kernel.

/proc/interrupts
Shows which interrupts are in use, and how many of each there have been.

/proc/ioports
Which I/O ports are in use at the moment.

/proc/kcore
An image of the physical memory of the system. This is exactly the same size as your physical memory, but does not really take up that much memory; it is generated on the fly as programs access it. (Remember: unless you copy it elsewhere, nothing under /proc takes up any disk space at all.)

/proc/kmsg
Messages output by the kernel. These are also routed to syslog.

/proc/ksyms
Symbol table for the kernel.

/proc/loadavg
The `load average' of the system; three meaningless indicators of how much work the system has to do at the moment.

/proc/meminfo
Information about memory usage, both physical and swap.

/proc/modules
Which kernel modules are loaded at the moment.

/proc/net
Status information about network protocols.

/proc/self
A symbolic link to the process directory of the program that is looking at /proc. When two processes look at /proc, they get different links. This is mainly a convenience to make it easier for programs to get at their process directory.

/proc/stat
Various statistics about the system, such as the number of page faults since the system was booted.

/proc/uptime
The time the system has been up.

/proc/version
The kernel version.
