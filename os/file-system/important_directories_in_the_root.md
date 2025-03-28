# Important directories in the root(/)
![](https://res.cloudinary.com/practicaldev/image/fetch/s--kjgxTg3h--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn.hashnode.com/res/hashnode/image/upload/v1647000231917/17qYbX3a3.png)
## boot
All the necessary files to boot the system and to carry out the startup process by the kernel

No permissions are here for normal use
## run
System processes use it to store temporary data for their own reasons
## bin
User binaries, executable files
Linux commands that are used in single user mode, and common commands that are used by all the users, like cat, cp, cd, ls...
## sbin
System binaries like fdisk, getty, ifconfig, reboot, route...
Super user reuqired
## etc
Configuration files(system-wide), which can generally be edited by hand in a text editor for example crontab, fstab, hostname, passwd...
user-specific configuration files are located in each user's home directory
## tmp
Necessary files that are temporarily required by the system as well as other software and applications running on the machine, files such as lock files and other data files
## lib, lib64
All helpful library files used by the system
These are used by an application or a command or a process for their proper execution(included in their headers and used by them)
Any kind of custom code that doesn't belong under controllers, models, or helpers
Kernel modules are drivers that make things like video card, sound card, WiFi, printer, and so on, work
## var
Contains variable data files - all files that change frequently, such as
* /log - a set of records that Linux maintains for the administrators to keep track of important events. They contain messages about the server, including the kernel, services and applications running on it
* /lock - lock files allows only one process to access the file in a specific time. It typically contains no data and only exists as an empty marker file, but may also contain properties and settings for the lock
* /spool - tasks waiting to be processed
* /tmp - temporary files saved between reboots
* /opt - variable data for installed packages
* /cache - application cache data
* /lib - data modified as programmes run
## srv
Contains data for servers
In the case if the system runs a server it will store its data in it(`/srv/http,/srv/ftp`)
## opt
Reserved for the installation of add-on(software that is not part of the system) application software packages

Another place where applications and libraries end up in is `/usr/local`, When software gets installed here, there will also be `/usr/local/bin` and `/usr/local/lib` directories
What determines which software goes where is how the developers have configured the files that control the compilation and installation process
## home
Personal files of a particular user of the system
Configuration files, documents, locally installed programs...
## root
Home directory of the root user
## usr
Originally it was where the home directories of the users were placed(usr/someone)
Currently it is where user-land programs and data
It also contains bin, sbin, lib... directories. 

Originally `/bin/` was created to store the minimum programs to be able to run a system and `usr/someone/bin` is for the programs which were installed manually by the user
Debian, Ubuntu, Mint... kept this but on the other hand for example Arch installs everything in `/bin/` and `usr/someone/bin` points to it
## proc
Virtual directory
contains information about the computer, such as information about the CPU and the kernel the system is running.
Files and directories are generated when computer starts, or on the fly, as the system is running and things change
## dev
Virtual directory
Files that represent devices that are attached to the local system
## sys
Virtual directory
Contains information from devices connected to your computer
## mnt
Manually mounted storage devices or partitions
## media
Subdirectories where removable media devices/external storages inserted into the computer are mounted
## cdrom
cdrom mount point
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjc3ODQwNjg4XX0=
-->