# <h1 style="text-align:center">Metasploit</h1>

## Introduction
The Metasploit Framework (MSF) is a prebuilt database of exploits for a variety of purposes. There are scripts for running reconnaissance, testing the existence of vulnerabilities (without compromising the target), tools for connecting to shells and running commands, etc. 

## Useful Commands

The most commonly used commands include:
rrrr
* ```msfconsole``` - start Metasploit.
* ```search exploit <vulnerability>``` - within MSF, search for a found vulnerability.
* ```use <full exploit path/name>``` - use the exploit.
* ```show options``` - view options available to configure; any option with ```Required``` set to ```yes``` needs to be set for the exploit to work.
* ```set <option> <option value>``` - set option values. 
* ```check``` - after setting options, run a check to see if server is vulnerable (not every exploit can do this).


## MSF Console Terms

* ```RHOSTS``` - the target IP (one IP, multiple IPs, or file containing list of IPs). 
* ```LHOST``` - listening host.