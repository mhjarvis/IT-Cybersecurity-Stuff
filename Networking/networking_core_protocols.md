# Networking Core Protocols

## DNS

The Domain Name System (DNS) is responsible for mapping a domain name to an IP address. DNS operates at the application layer. It uses port UDP port 53 by default and TCP port 53 as a default fallback.

4 common types of DNS records:

1. `A record` - the Address record maps a hostname to one or more IPv4 addresses.
2. `AAAA Record` - similar to `A record` but it is meant for IPv6.
3. `CNAME Record` - maps a domain name to another domain name. For example, www.ex.com can be mapped to ex.com or ex.org.
4. `MX Record` - The Mail Exchange record specifies the mail server responsible for handling emails for a domain.
