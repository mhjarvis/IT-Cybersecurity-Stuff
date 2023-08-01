# <h1 style="text-align:center">Network Mapper (nmap)</h1>

## Introduction
```nmap``` is an open-source command-line tool that is used to scan IP addresses and ports that will detect installed applications and find open ports and service. It uses raw IP packets to determine what hosts are available, what services (application name and version) are running, what operating system is running, what type of packet filters/firewalls are in use, etc. 

Port state has one of four options.
- open - means that an application on the target machine i listening for connections/packets on that port.
- filtered - means that a firewall, filter, or other network obstacle is blocking the port so that Nmap cannot tell whether it is open or closed.
- closed - have no applications listening on them, though they could open up at any time.
- unfiltered - when they are responsive to Nmap's probes, but Nmap cannot determine whether they are open or closed. 

    nmap [OPTIONS] {target_IP}

Common options:

    -sC     // equialent to --script=default
    -sV     // probes open ports to determine service/version information
    -Pn     // treat all hosts as online; skip host discovery