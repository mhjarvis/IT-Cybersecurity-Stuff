# <h1 style="text-align:center">Nmap</h1>

## Introduction

By default (without any options) Nmap will scan only the 1,000 most common ports. It will also, by default, conduct a TCP scan unless specificlly requested. 

## Commands
```nmap -sV --open -oA <filename> <target_IP>``` - run scan and save content as ```<filename>```.

## Options

* ```-sC``` - specifies that Nmap scripts should be used to try and obtain more detailed information.
* ```-sV``` - instructs Nmap to perform a version scan; Nmap will fingerprint services and id service protocol, app name, and version.
* ```-p-``` - tells Nmap that we want to scan all 65,535 ports.
* ```-p <port,port,port>``` - scan specific ports, seperated by a comma.
* ```nmap --script <scipt name> -p<port> <host>``` - run a specific script. 
* ```nmap -sV --script=banner <target>``` - attempt to grab banners of target IP (can also use Netcat). 
* ```nmap -v -oG -``` - outputs which ports nmap scans for a given scan type (run without commands).

* ```nmap -sV -sC -p- [target_IP]``` - scan all ports of target.


* ```-sV``` - service enumertion scan against top 1,000 ports.
* ```-open``` - return only open ports.
* ```-oA``` - output all scan formats (XML, greppable, text output). 

## Scan Types
```TCP Connect scans``` (```-sT```) will attempt a TCP handshake with each target port. Nmap can establish if a port is closed if it receives a TCP packet back with the RST (Reset) flag set. It is open if Nmap get a TCP/ACK packet back. If a port is protected by a firewall, the packet may get droped and Nmap will receive nothing back, meaning it will be considered 'filtered'. Of course, firewalls can be configured to reject incoming TCP connections with a RST TCP packet.

```SYN Scans``` (```-sS```) are used to scan the TCP port-range of a target. SYN scans will send back a RST TCP packet to stop requests from the target. These scans may not get logged by IDS and can be faster. However, they require sudo permissions and may bring down unstable services. These are the default scans if Nmap is run with 'sudo', otherwise Nmap runs TCP Connect scans. 

```UDP Scans``` (```-sU```) are generally slower. When a packet is sent to an open port, there should be no response (```open|filtered```). If there is a response (unusual), the port is marked as open. When sent to a closed port, the target should respond with a ICMP (ping) packet. 

```NULL, FIN and Xmas TCP Scans``` tend to be stealthier. Null scans (```-sN```) is when a TCP request is sent with no flags set. The host should respond with a RST if it is closed. FIN scans (```-sF```) send a request iwth the FIN flag set. RST is sent if the port is closed. Xmas scans (```-sX```) send a malformed TCP packet and expects a RST response for closed ports. The ```PSH```, ```URG```, and ```FIN``` flags are set. If the port is open for any of these scans, there is no response. 

```ICMP Network Scanning``` or a ```ping sweep``` is a way to enumerate a network by sending an ICMP packet to each possible IP address on the network. This is done with the ```-sn``` switch. 

    nmap -sn <target_IP>

The ```-sn``` switch tells Nmap not to scan any ports.

## Web Enumeration

* ```nmap -sV --script=http-enum <target_IP>``` enumerates web directories used by popular web applications; [link](https://nmap.org/nsedoc/scripts/http-enum.html).

## Notes

* Note the ```-sC``` flag reports on the ```http-server-header``` and the ```http-title``` for any webpage hosted on a webserver. 
