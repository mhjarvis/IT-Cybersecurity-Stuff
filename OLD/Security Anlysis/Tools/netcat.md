# <h1 style="text-align:center">Netcat</h1>

## Introduction
Netcat (ncat, nc) is a network utility for interacting with TCP/UDP ports. It is primarily used to connect to shells. It can also connect to any listening port and interact with the service running on that port.

    netcat 10.10.10.10 22                   // connect on port 22 (ssh)

The responding port may send us a ```banner```, stating that a service is running on it. This technique is called ```Banner Grabbing``` which can help identify what service is running on that port. Netcat can also be used to transfer files between machines. We can also use the ```nc``` version of Netcat.

* ```nc -nv <target IP> <port number>``` - nc version of Netcat.
* ```nc -lvnp <port number>``` - start a netcat listener on a port of our choosing; for establishing a reverse shell.
* 

## Flags

* ```-l``` - listen mode; to wait for a connection to connect to us.
* ```-v``` - verbose mode; tells us when we receive a connection.
* ```-n``` - disable DNS resolution and only connect from/to IPs, to speed up the connection.
* ```-p <port number>``` - port number ```netcat``` is listening on, and the reverse connection should be sent to.