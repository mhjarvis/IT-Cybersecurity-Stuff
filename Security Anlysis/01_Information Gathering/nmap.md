# <h1 style="text-align:center">Nmap</h1>

## Introduction


By default (without any options) Nmap will scan only the 1,000 most common ports. It will also, by default, conduct a TCP scan unless specificlly requested. 

## Helpful Options

* ```nmap -sC``` - specifies that Nmap scripts should be used to try and obtain more detailed information.
* ```nmap -sV``` - instructs Nmap to perform a version scan; Nmap will fingerprint services and id service protocol, app name, and version.
* ```-p-``` - tells Nmap that we want to scan all 65,535 ports.
* ```-p <port,port,port>``` - scan specific ports.
* ```nmap --script <scipt name> -p<port> <host>``` - run a specific script. 
* ```nmap -sV --script=banner <target>``` - attempt to grab banners of target IP (can also use Netcat). 
* ```nmap -v -oG -``` - outputs which ports nmap scans for a given scan type (run without commands).

* ```nmap -sV -sC -p- [target_IP]``` - scan all ports of target.


#### ```nmap -sV --open -oA <filename> <target_IP>```. 
* ```-sV``` - service enumertion scan against top 1,000 ports.
* ```-open``` - return only open ports.
* ```-oA``` - output all scan formats (XML, greppable, text output). 

## Web Enumeration

* ```nmap -sV --script=http-enum <target_IP>``` enumerates directories used by popular web applications; [link](https://nmap.org/nsedoc/scripts/http-enum.html).

## Notes

* Note the ```-sC``` flag reports on the ```http-server-header``` and the ```http-title``` for any webpage hosted on a webserver. 
