# <h1 style="text-align:center">Linux Fundamentals</h1>

## Linux Structure

Linux follows five core principles:

1. Everything is a file - all configuration files for various services that make Linux run are stored in text files. 
2. Small, single-purpose programs - numerous tools that work well together.
3. Ability to chain programs together to perform complex tasks - integration of different tools allow us to carry out complex tasks.
4. Avoid captive user interfaces - Linux is designed to work with the shell which provides increased control of the OS.
5. Configuration data stored in a text file - e.g. ```/etc/passwd``` stores all users on the system.

Linux components consist of:

1. Bootloader - code that guides the boot process (e.g. GRUB).
2. Kernel - main component of the OS; manages resources for the systems I/O devices at hardware level.
3. Daemons - background services; make sure key functions are working correctly; load after boot. 
4. OS Shell - CLI; interface between OS and User. 
5. Graphics server - provides graphical sub-system (e.g. 'X' or 'X-server').
6. Window Manager - GUI (e.g. GNOME, KDE, MATE, etc.). 
7. Utilities - programs.

Linux can be broken down into layers:

1. Hardware - RAM, CPU, hard drive, etc.
2. Kernel - core of Linux; virtualize and control hardware, allocate memory, etc.; gives each process its own virtual resources and prevents/mitigatees conflicts between different processes.
3. Shell - CLI.
4. System Utility - makes available the OS' functionality. 

Important directories or paths in Linux include: 

* ```/``` - root; top-level directory that contains files required to boot the OS before other file systems are mounted as well as files required to boot other fileshystems. After boot, all other filesystems are mounted at standard mount points as subdirectories of the root.
* ```/bin``` - contains essential command binaries.
* ```/boot``` - static bootloader, kernel executable, and files required to boot Linux.
* ```/dev``` - device files to facilitate access to every hardware device attached to the system.
* ```/etc``` - system config files; also may contain config files for installed apps.
* ```/home``` - each user has subdirectory here for storage.
* ```/lib``` - shared library files required for boot.
* ```/media``` - external removable media (e.g. USB) are mounted here.
* ```/mnt``` - temp mount point for regular filesystems.
* ```/opt``` - optional files (third-party tools can be saved here).
* ```/root``` - home directory for the root user.
* ```/sbin``` - contains executables used for system administration (binary sys files).
* ```tmp``` - temporary file storage; generally cleared on boot.
* ```usr``` - executables, libraries, man files, etc.
* ```var``` - variable files such as log files, email in-boxes, web app related files, cron files, etc.

## Bash

Customization can happen in the shell's configuration file ```.bashrc```.

## System Information

* ```hostname``` - lists computer we are logged into.
* ```whoami``` - current username.
* ```id``` - adds group membership and ids.
* ```uname``` - print system information; ```-r``` can id the kernel for exploits.
* ```pwd``` - working directory.
* ```ifconfig```- network interface.
* ```ip``` - show or manipulate routing.
* ```netstat``` - show network status.
* ```ss``` - utility to investigate sockets.
* ```ps``` - shows process status.
* ```who``` - displays who is logged in.
* ```env``` - prints environment or sets and executes command.
* ```lsblk``` - lists block devices.
* ```lsusb``` - lists usb devices.
* ```lsof``` - lists opened files.
* ```lspci``` - lists pci devices.