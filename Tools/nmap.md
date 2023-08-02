# <h1 style="text-align:center">Nmap</h1>

## Introduction


By default (without any options) Nmap will scan only the 1,000 most common ports. It will also, by default, conduct a TCP scan unless specificlly requested. 

## Helpful Options

* ```nmap -sC``` - specifies that Nmap scripts should be used to try and obtain more detailed information.
* ```nmap -sV``` - instructs Nmap to perform a version scan; Nmap will fingerprint services and id service protocol, app name, and version.
* ```nmap -p-``` - tells Nmap that we want to scan all 65,535 ports.





## Helpful Cmmands

* ```nmap -sV -sC -p- [target_IP]```