## Connecting

Download the OpenVPN file.

    sudo openvpn {.ovpn_file}

## Meow

```Enumeration``` - documenting the current state of the target to learn as much as possible about it. 

The first steps in the Enumeration phase involve scanning for open ports to see what potential opportunities there are (using ```nmap``` (Network Mapper), for example).  We can also use ```ping``` on the target's IP address to see if our packets are reaching their destination. ```nmap``` works by sending requests to a target's ports in hopes of receiving a reply, determining if that port is open or not. 

    sudo nmap -sV {target_IP}               // -sV determines name/description of identified services

    telnet {target_IP}                      // start a telnet session with target

There is a small chance that a username exists without a password (or a blank password), in which case you can try some default users (e.g. 'admin', 'administrator', 'root').

# Fawn

FTP or File Transfer Protocol is often misconfigured, especially when not correctly understood. FTP can be used to transfer log files from one network device to another (or a log collection server). If not secured, these logs can provide valuable information to allow someone to map out the network, enumerate usernames, detect active services, etc. 