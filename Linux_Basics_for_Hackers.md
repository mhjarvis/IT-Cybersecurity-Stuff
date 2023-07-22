<h1 style="text-align:center">Getting Stated with the Basics</h1>

## The Linux Filesystem

    /root - home directory of the root user
    /etc - contains the Linux configuration files ( controls how programs start)
    /home - user's home directory
    /mnt - where other filesystems are attached or mounted to the filesystem
    /media - where cds and usb devices are attached / mounted to the filesystem
    /bin - application binaries reside here
    /lib - libraries

## Basic Commands

    pwd - shows where you are currently located
    whoami - shows which user you are loggd in as
    cd - use to move between directories
    cd ../.. - move up two levels
    ls - see contents of a directory  (list)
        -l - gets more info about files (long listing)
        -a - shows hidden files
        --help / -h / ? - show the dedicated help file
    man - shows the referencing manual
    locate [keyword] - will go through entire filesystem and locate every occurence of that word
    whereis [keyword] - returns location, source, and man page of the binary
    which [keyword] - returns location of binaries in teh PATH variable in Linux

    find [directory] [option] [expression] - e.g (find / -type f -name apache2)

## Wildcards

    ? - respresents a single character
    [] - wildcard matches the letters inside the array
    * - matches any character of any length

## Filtering with ```grep```

```grep``` is often used when output is piped from one command to another. In other words, we can take the output of one command and send it as input to another command. We use the ```|``` to do this.

    ps - displays information about processes running on the machine
    ps aux - provides a listing of all process running in the system

Using ```grep``` we can narrow down the list of processes to see if specific processes are running. For example:

    ps aux

## Creating 

    cat > [filename] - creates a new file and will go into interactive mode; ctrl-D will exit the prompt

    cat >> [filename] - append additional text
    cat > [filename] - will overwrite if file exists

    touch [filename] - create new file
    mkdir [newdirectory] - create new directory
    cp oldfile [directory for newfile] - copy file to new directory

When copying the new file, renaming is optional. 

    mv newfile [directory] - move file without copying
    mv newfile newfile2 - rename file

    rm [filename] - remove a file
    rmdir [directoryname] remove directory (must be empty)
    rmdir -r [directoryname] - removes directory even with file in it

<h1 style="text-align: center">Text Manipulation</h1>

    head [filename] - by default, show the first 10 lines of a file
    head -20 [filename] - display the first 20 lines
    tail [filename] - last 10 lines of a file
    tail -20 [filename] - display the last 20 lines
    tail -n -20 [filename] - same as above

## Numbering Lines

    nl [directory location] - provide line numbers (nl paswd)
    sed - stream editor; find and replace

For working with larger files you have the ```more``` and ```less``` commands.

    more [filename] - display a page of the file at a time, page through with ENTER
    less [filename] - adds ability to filter output by terms
        / - provides prompt to search for keywords
        n - goes to the next occurence of the pattern

<h1 style="text-align: center">Analyzing and Managing Networks</h1>

    ifconfig - query your active network connections
        inet - IP address currently assigned to network interface
        broadcast - address used to send out info to all IPs on the subnet
        netmask - determines what part of the IP aaddress is connected to local network

```ifconfig``` also shows the loopback address (called ```lo```), also called ```localhost```. This is a special software address that connects you to your own system. Software and services that are not running on your system cannot use it. It would be used to test something on your system, such as your own web server.

    iwconfig - gets information on wireless adapters
        Access Point - how its connected to internet (router MAC)

## Changing Your IP Address

    ifconfig [interfacetochange - eth0] [newIP] 
    ifconfig eth0 192.168.181.115 - will need to be in super user mode

## Changing Netork Mask and Broadcast Address

    ifconfig wlan0 192.168.111.111 netmask 255.255.0.0 broadcast 192.168.1.255

This will trigger a new command prompt at which point you enter ifconfig again to verify that each parameter has changed correctly.

## Spoofing Your MAC Address

    ifconfig eth0 down - take down interface
    ifconfig eth0 h2 ether 00:11:22:33:44:55 - hw for hardware or ether for Ethernet
    ifconfig eht0 up - bring interface back up

## Assigning New IP Address via DHCP

Dynamic Host Configuration Protocol is used to automatically assign IP addresses to hosts. In small networks, a router might do this. A ISP will also use DHCP to assign IP addresses (which your router will normally get). DHCP also keeps a log file that tracks what IP address is assigned to a system.

IF you are setting a static IP address, you must then return and get a new DHCP-assigned IP address. 

You make a call to DHCP with ```dhclient``` followed by the interface you want th address assigned to.

    dhclient -r wlan0 - removes any leases you currently have

    dhclient wlan0 - reissue IP address

## Examining DNS with ```dig```
Getting DNS information can be valuable in early-on exploration and information gathering. 

    dig hackers-arise.com ns
    dig hackers-arise.com mx - mx option is for mail exchange

<h1 style="text-align: center">Adding and Removing Software</h1>

## Installing Software with ```apt-get```

For Debian-based distros (e.g. Kali, Ubuntu), Advanced Packaging Tool (apt) is the default. ```apt-get``` is the primary command. 

    apt-cache search [keyword]          // check whether the package is in your repo
    apt-get install [packagename]       // install software
    apt-get remove [packagename]        // uninstall
    apt-get purge [packagename]         // remove config files as well
    apt autoremove [packagename]        // remove dependencies

    apt-get update                      // check for updates
    apt-get upgrade                     // upgrade your system 

## Your ```sources.list``` File

```sources.list``` notes what repositories your system will search for software. Here you can add additional repositories to search through. 

    cd /etc/apt/sources.list        // located in /etc which contains config files

## Installing Software with ```git```

    git clone [github URL]      // copies all data/files from repo to your system

<h1 style="text-align: center">Controlling File and Directory Permissions</h1>

## File Permissions

    chown [username] [filelocation]     // change user ownership of a file
    chgrp [groupname] [filelocation]    // change group ownership of a file

    Binary  Octal   rwx
    000     0       ---
    001     1       --x
    010     2       -w-
    011     3       -wx
    100     4       r--
    101     5       r-x
    110     6       rw-
    111     7       rwx

```chmod``` uses the above octal values to change file permissions for the owner, group, and everyone else (other).

    chmod [owner group other] [filename]
    chmod 777 test.txt               // give everyone  rwx permissions
     
File permissions can also be changed with UGO (user, group, others) syntax.     

    u = user
    g = group
    o = other

    - remove permission
    + add permission
    = set permission

    chmod u-w test.txt          // user remove write permission
    chmod u+x, o+x test.txt     // multiple permission changes

When downloading neww tool, keep in mind that Linux will assign all files/permissions default permissions of ```666``` (for files) and ```777``` (for directories). To fix this problem, you will need to give yourself root access and update thesse permissions.

## Masks

You can change the default permissions allocated to files and directories with the ```umask``` method. This allows you to remove permissions from the base permissions. The ```umask``` number is subtracted from the permissions number to give the new permission status. 

    umask                       // show the current unmask number
    /home/username/.profile     // file to edit the umask value in

## Special Permissions

Set the ```SUID``` with a `4` before the regular permissions, which gives any user the permission to execute the file with the permissions of the owner. 

    chmod 4664 [filename]       // set SUID with a '4'
    chmod 2664 [filename]       // set SGID with a '2'

These are sometimes set by developers, especially for files that interact with root privelages a lot, which may lead to privelage escalation.

# <h1 style="text-align: center">Process Management</h1>

Understanding how to find processes amongst the hundreds of processes running simultaneously is a critical skill. Think of finding the anti-virus process and terminating it. 

## Viewing Processes
```ps``` displays information about a selection of the active processes. ```top``` instead provides a repetitive update of the selection. 

    ps              // reports a snapshot of the current processes

Note that the ```PID``` (first column) is a unique process ID that is assigned sequentially as processes are run. 

    ps aux          // shows all processes running on the system for all users

Note:
- ```User``` - the user who invoked the process
- ```PID```  - the process ID
- ```%CPU``` - the percent of CPU this process is using
- ```%MEM``` - the percent of memory this process is using
- ```COMMND``` - the name of the command that started the process





<h1 style="text-align: center"></h1>
<h1 style="text-align: center"></h1>
<h1 style="text-align: center"></h1>
<h1 style="text-align: center"></h1>
<h1 style="text-align: center"></h1>
<h1 style="text-align: center"></h1>
<h1 style="text-align: center"></h1>
