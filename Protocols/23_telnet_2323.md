# <h1 style="text-align:center">Telnet</h1>

## Introduction
The first steps in the Enumeration phase involve scanning for open ports to see what potential opportunities there are (using ```nmap``` (Network Mapper), for example). Ports allow us to run multiple services at once using just one IP address. We can also use ```ping``` on the target's IP address to see if our packets are reaching their destination. ```nmap``` works by sending requests to a target's ports in hopes of receiving a reply, determining if that port is open or not. 

    sudo nmap -sV {target_IP}               // -sV determines name/description of identified services

    telnet {target_IP}                      // start a telnet session with target

There is a small chance that a username exists without a password (or a blank password), in which case you can try some default users (e.g. 'admin', 'administrator', 'root').