<h1 style="text-align:center">Subdomain Enumeration</h1>

Subdomain enumeration is the process of finding valid subdomains for a domain to further expand the attack surface and to discover other points of vulnerability.

## OSINT - Open Source Intelligence

### SSL/TLS Certificates

When a SSL certificate is created for a domain by a Certificate Authority, the Certificate Authority takes part in Certificate Tranparency logs. These are public. They are meant to stop malicious/accidentally made certificates, but can be used to discover subdomains.

Searchable domains:

- https://crt.sh/
- https://ui.ctsearch.entrust.com/ui/ctsearchui

### Search Engines

Use advanced search methods via Google.

`site:*.domain.com -site:www.domain.com` - only provides results leading to domain.com.

## DNS Bruteforce

Bruteforce DNS enumeration involves trying numerous lists against possible subdomains. Tools such as `dnsrecon`.

## Sublist3r

Sublist3r uses automated scripts to discover subdomains. It searches various search engines to find subdomains.

https://github.com/aboul3la/Sublist3r

## Virtual Hosts

Some subdomains are not hosted on publically accessible DNS results. A web server knows which webiste a client wants based on the `Host` header. This `Host` header can be altered and monitored to see if a new website is discovered. To do so, a wordlist can be used.

Using `fuff`:

`ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://MACHINE_IP`

`ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://MACHINE_IP -fs {size}`
