# <h1 style="text-align:center">Gobuster</h1>

## Introduction
```Gobuster``` allows DNS, vhost, an directory brute-forcing. It can help find hidden functionality or pages/directories exposing sensitive information. It also alows for enumeration of public AWS S3 buckets. 

## Useful Commands

* ```gobuster dir -u http://<target_IP>/ -w /usr/share/dirb/wordlists/common.txt``` - scan using the dirb common.txt wordlist.

Clone the SecLists repo and install to use DNS. 

    git clone https://github.com/danielmiessler/SecLists
    sudo apt install seclists -y
    gobuster dns -d inlanefreight.com -w /usr/share/SecLists/Discovery/DNS/namelist.txt


## Notes

* ```Gobuster``` will list directories with status codes clarifying access to the resource (200 - successful, 301 - redirect, 403 - forbidden). 

## See Also

* [HTTP Status Codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)
* ```fuff``` - similar program as ```GoBuster```.
