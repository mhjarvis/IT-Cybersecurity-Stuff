## Connecting

Download the OpenVPN file.

    sudo openvpn {.ovpn_file}

    sudo killall openvpn        // end all sessions

## Shells

* ```Reverse shell``` -initiates a connection back to a 'listener' on our attack box.
* ```Bind shell``` - binds to a specific port on the target host and waits for a connection from our attack box.
* ```Web shell``` - runs os commands via the web browser, typically not interactive or semi-interactive.

## Meow

```Enumeration``` - documenting the current state of the target to learn as much as possible about it. 

The first steps in the Enumeration phase involve scanning for open ports to see what potential opportunities there are (using ```nmap``` (Network Mapper), for example). Ports allow us to run multiple services at once using just one IP address. We can also use ```ping``` on the target's IP address to see if our packets are reaching their destination. ```nmap``` works by sending requests to a target's ports in hopes of receiving a reply, determining if that port is open or not. 

    sudo nmap -sV {target_IP}               // -sV determines name/description of identified services

    telnet {target_IP}                      // start a telnet session with target

There is a small chance that a username exists without a password (or a blank password), in which case you can try some default users (e.g. 'admin', 'administrator', 'root').

# Fawn

FTP or File Transfer Protocol is often misconfigured, especially when not correctly understood. FTP can be used to transfer log files from one network device to another (or a log collection server). If not secured, these logs can provide valuable information to allow someone to map out the network, enumerate usernames, detect active services, etc. FTP works on port 21. To better secure file transfer, you could move services to port 22 and use SSH to tunnel information and add encryption.

    ftp {target_IP}         // will attempt to connect to the ftp server

A typical misconfigured ftp service allows a ```anonymous``` account to access the service like any other authenticated user. This username can login with any password you want, since the service will disregard the passord for this specific account. 

    ftp>: passive           // set passive mode
    ftp>: get data.txt      // transfer file to your system

Using passive mode for data transfers allows use of ftp in environments where a firewall prevents connections from the outside world back to the client machine (PASV).

## Dancing

SMB or Server Message Block is another way to transfer files betwween two hosts. This protocol provides shared access to files, printers, and serial ports betwween endpoints. We mostly see this on Windows machines. Usually this means port 445 TCP will be open. SMB usually runs at the Application or Presentation layer. It is used most often ith NetBIOS over TCP/IP (NBT) which works on the Transport layer. 

SMB allows applications (or the user) access files at a remote server, along with other resources such as printers. It can read, create, and update files on that remote server. SMB-enabled storage on the network i called a ```share```. If someone has the address of the server and proper credentials, they have access. Admins may make mistakes here and accidentally allow logins without any valid credentials (or by using ```gues accounts``` or ```anonymous log-ons```). SMB is on port 445. 

SMB authentication always requires a username and will use your host machines name if you do not give it one.

    sudo smbclient -L {target_IP}
    sudo smbclient \\\\{target_IP}\\{username}
    sudo 