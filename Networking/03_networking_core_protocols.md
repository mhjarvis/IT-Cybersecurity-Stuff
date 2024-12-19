# Networking Core Protocols

## DNS

The Domain Name System (DNS) is responsible for mapping a domain name to an IP address. DNS operates at the application layer. It uses port UDP port 53 by default and TCP port 53 as a default fallback.

4 common types of DNS records:

1. `A record` - the Address record maps a hostname to one or more IPv4 addresses.
2. `AAAA Record` - similar to `A record` but it is meant for IPv6.
3. `CNAME Record` - maps a domain name to another domain name. For example, www.ex.com can be mapped to ex.com or ex.org.
4. `MX Record` - The Mail Exchange record specifies the mail server responsible for handling emails for a domain.

## WHOIS

`whois _address` - command will allow you to find out registrar information.

## HTTP(S)

Common commands/methods

`GET`, `POST`, `PUT`, `DELETE`.

## FTP

FTP listens on port 21 by default.

`USER` - used to input the username.
`PASS` - used to enter the password.
`RETR` - used to download file from the FTP server to client.
`STOR` - used to upload file from client to FTP server.

```bash
ftp ip_address                          // connect to server via ftp
```

FTP file transfers are saved to the directory FTP was launched from.

## SMTP

Simple Mail Transfer Protocol defines how a mail client talks with a mail server and how a mail server talks with another.

Commands used:

`HELO` or `EHLO`
`MAIL FROM` - specifies the sender's email address.
`RCPT TO` - specifies the recipient's email address.
`DATA` - indicates that the client will begin sending the content of the email message.
`.` - is sent on a line by itself to indicate the end of the.

## POP3

`Post Office Protocol version 3` is designed to allow the client to communicate with a mail server and retrieve email messages.

`USER <username>` - identifies the user
`PASS <password>` - provides the user’s password
`STAT` - requests the number of messages and total size
`LIST` - lists all messages and their sizes
`RETR <message_number>` - retrieves the specified message
`DELE <message_number>` - marks a message for deletion
`QUIT` - ends the POP3 session applying changes, such as deletions
