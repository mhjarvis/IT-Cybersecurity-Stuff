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

## Kernel Exploits

