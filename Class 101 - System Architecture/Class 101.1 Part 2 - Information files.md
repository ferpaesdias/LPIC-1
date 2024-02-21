# Class 101.1 Part 2 - Information files

## Glossary

**DMA** => Direct memory access.   

`/proc/` => Common groups of kernel-related information.  
`/sys/` => The */sys/* directory contains information similarly maintained in */proc/*, but displays a hierarchical view of device-specific information regarding hot plug devices.   
`udev` => responsible for identifying and configuring devices already present during machine startup (coldplug detection) and devices identified while the system is running (hotplug detection). Udev uses SysFS, the pseudo file system mounted on /sys for hardware-related information. As new devices are detected, udev searches the predefined rules stored in the `/etc/udev/rules.d/` directory for a matching rule. The most important rules are provided by the distribution, but it is possible to add new ones for specific cases. 


`/proc/cpuinfo` => Detailed CPU information.   
`/proc/interrupts` => This file records the number of interrupts per IRQ.      
`/proc/ioports` => Lists the currently registered port regions used for inbound or outbound communication with a device.   
`/proc/dma` => This file contains a list of registered ISA DMA channels in use.   
`/proc/meminfo` => Memory information.   
`/proc/partitions` => This file contains partition block allocation information.   
`/proc/uptime` => Reports detailing how long the system has been on since the last reboot.   
`/proc/version` => This file specifies the version of the Linux kernel and *gcc* in use.   

`/etc`