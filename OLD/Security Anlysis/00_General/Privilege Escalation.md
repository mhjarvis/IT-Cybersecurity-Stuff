# <h1 style="text-align:center">Privilege Escalation</h1>

Initial access to a remote host is usually low-privilege. To gain full access, we would need to find a inernal/local vulnerability to escelate privelages to ```root``` (Linux) or ```administrator/System``` (Windows).

## PrivEsc Checklists

After initial access, we want to enumerate a host to find any additional vulnerabilities. One way to do so is to use a checklist. 

[HackTricks](https://book.hacktricks.xyz/welcome/readme)

[HackTricks - Linux Privilege Escalation](https://book.hacktricks.xyz/linux-hardening/linux-privilege-escalation-checklist)

[HackTricks - Windows Privilege Escalation](https://book.hacktricks.xyz/windows-hardening/checklist-windows-privilege-escalation)

[PayloadsAllTheThings - Linux Privilege Escalation](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-%20Privilege%20Escalation.md)

[PayloadsAllTheThings - Windows Privilege Escalation](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md)

## Enumeration Scripts

Scripts can be run to enumerate the server. The following scripts create a lot of 'noise' that may trigger security software. 

[LinEnum - Linux](https://github.com/rebootuser/LinEnum)

[linuxprivchecker - Linux](https://github.com/sleventyeleven/linuxprivchecker)

[Seatbelt - Windows](https://github.com/GhostPack/Seatbelt)

[JAWS - Windows](https://github.com/411Hall/JAWS)

[Privilege Escalation Awesome Scripts SUITE (PEASS) - Windows/Linux](https://github.com/carlospolop/PEASS-ng)

## Kernel Exploits and Vulnerable Software

Old operating systems may carry vulnerabilitiies, especially if they are unpatched. Note that kernel exploits can cause system instability. Also look for installed software as there are possibly public exploits on software, especially in older versions.

* ```dpkg -l``` - show installed software on Linux.
* ```C:\Program Files``` - see installed software on Windows.

## User Privileges

Users may have privileges. Common ways to exploit certain user privileges include:
1. ```sudo``` - allows lower privileged users to execute as root without giving access to root.
        
        sudo -l                     // check what privilegas a user has
        sudo su -                   // switch to root
        sudo -u user <command>      // run command as user
        
2. SUID
3. Windows Token Privileges

[GTFOBins - list of commands and how they can be exploited through sudo.](https://gtfobins.github.io/)

[LOLBAS - list of Windows applications that may be leveraged.](https://academy.hackthebox.com/module/77/section/844)

## Scheduled Tasks

Scheduled task can be taken advantage of:

1. Add new scheduld tasks/cron jobs.
2. Trick them to execute a malicious software.

Cron jobs are a common way Linux maintains scheduled tasks. We can check write permissions via:

1. /etc/crontab
2. /etc/cron.d
3. /var/spool/cron/crontabs/root

If we are able to write to a directory with cron jobs, we can write a bash script with reverse shell command.

## Exposed Credentials

Many files may contain exposed credentials, especially with configuration files, log files, and user history files (bash_history in Linux; PSReadLine in Windows). 

## SSH Keys

If there is read access over the .ssh directory for a user, we may read private ssh keys found in ```/home/user/.ssh/id_rsa``` or ```/root/.ssh/id_rsa```. 

    vim id_rsa                      // read file
    chmod 600 id_rsa
    ssh user@<target_IP> -i id_rsa

If we find ourselves with write access to a users/.ssh/ directory, we can place our public key in the user's ssh directory at /home/user/.ssh/authorized_keys. This technique is usually used to gain ssh access after gaining a shell as that user. The current SSH configuration will not accept keys written by other users, so it will only work if we have already gained control over that user. We must first create a new key with ssh-keygen and the -f flag to specify the output file:

    ssh-keygen -f key

This will give us two files: key (which we will use with ssh -i) and key.pub, which we will copy to the remote machine. Let us copy key.pub, then on the remote machine, we will add it into /root/.ssh/authorized_keys:

    user@remotehost$ echo "ssh-rsa AAAAB...SNIP...M= user@parrot" >> /root/.ssh/authorized_keys

Now, the remote server should allow us to log in as that user by using our private key:

    ssh root@<target_IP> -i key

As we can see, we can now ssh in as the user root. The Linux Privilege Escalation and the Windows Privilege Escalation modules go into more details on how to use each of these methods for Privilege Escalation, and many others as well.

