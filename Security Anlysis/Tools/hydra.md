

Hydra is a fast online password cracking tool that can perform rapid dictionary attacks. 

    hydra -t 4 -l dale -P /usr/share/wordlists/rockyou.txt -vV 10.10.10.6 ftp

* ```hydra``` - runs the hydra tool
* ```-t 4``` - number of parallel connections per target
* ```-l [user]``` - points ot the user who's account your trying to compromise
* ```-P [path to dictionary]``` - points to the file containing the list of passwords
* ```-vV``` - sets verbose mode showing each attempt
* ```[machine IP]``` - IP address of target machine
* ```ftp / protocol``` - sets the protocol


