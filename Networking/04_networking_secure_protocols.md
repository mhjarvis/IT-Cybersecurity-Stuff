<h1 style="text-align:center">Networking Secure Protocols</h1>

## Protocol Limitations

- **Confidentiality**:
  - Data is not encrypted, allowing third parties to read sensitive information like passwords or credit card details sent over HTTP.
  - Email attachments or private documents sent via plain protocols are also accessible to attackers.
- **Integrity**:
  - Data can be modified during transmission (e.g., a payment of 100 pounds can be altered to 800 pounds).
- **Authenticity**:
  - No guarantee that the server you communicate with is legitimate, making phishing and data interception possible.

## Enhancing Security with TLS

- **TLS (Transport Layer Security)**:
  - Secures data transfer by ensuring **confidentiality**, **integrity**, and **authenticity**.
  - Upgrades protocols to their secure counterparts:
    - `HTTP → HTTPS`
    - `POP3 → POP3S`
    - `SMTP → SMTPS`
    - `IMAP → IMAPS`

## Replacing TELNET with SSH

- **TELNET**: Insecure due to plaintext data transmission.
- **SSH (Secure Shell)**:
  - Provides secure remote system access via encryption.
  - Offers extensible security features for other protocols.

# TLS and Secure Communication

## Early Challenges

- **Packet Capturing**:
  - Attackers could set their network card to promiscuous mode to capture all network traffic.
  - Passwords, emails, and chats were often sent in plaintext, making them easy to intercept.
  - Users had no means to prevent login credentials from being exposed.

## Evolution of Secure Communication

- **SSL (Secure Sockets Layer)**:
  - Developed by Netscape in the early 1990s.
  - **SSL 2.0**: Released in 1995 as the first public version.
- **TLS (Transport Layer Security)**:
  - Introduced in 1999 by the Internet Engineering Task Force (IETF).
  - **TLS 1.3**: Released in 2018, providing significant protocol improvements.
  - Built upon SSL but offers enhanced confidentiality, integrity, and security.

## Importance of TLS

- Operates at the transport layer of the OSI model.
- Secures client-server communication over insecure networks.
- Ensures:
  - **Confidentiality**: Data cannot be read by third parties.
  - **Integrity**: Data cannot be altered during transmission.
- Applications:
  - Online shopping, banking, messaging, and email rely on TLS for secure operations.

## Protocol Upgrades with TLS

- Common protocols enhanced with TLS:
  - `HTTP → HTTPS`
  - `DNS → DoT (DNS over TLS)`
  - `MQTT → MQTTS`
  - `SIP → SIPS`

## TLS Certificates

- **Certificate Signing**:
  - A server (or client) generates a Certificate Signing Request (CSR).
  - Submitted to a Certificate Authority (CA) for verification.
  - CA issues a digital certificate confirming authenticity.
- **Trusted Certificates**:
  - Hosts need trusted CA certificates installed to validate server identities.
  - Free certificates available via providers like Let's Encrypt.
- **Self-Signed Certificates**:
  - Cheaper but lack third-party verification, reducing trustworthiness.

# HTTP and HTTPS Overview

## HTTP: Hypertext Transfer Protocol

- **Characteristics**:
  - Operates over **TCP** on port 80 by default.
  - Sends data in plaintext, making it vulnerable to interception.
- **Process**:

  1. Resolve the domain name to an IP address.
  2. **TCP Three-Way Handshake**:
     - Initiates a connection between the client and server.
  3. **HTTP Communication**:
     - Sends requests (e.g., `GET / HTTP/1.1`) and receives responses.
  4. **TCP Connection Termination**:
     - Closes the connection.

- **Security Concern**:
  - Plaintext data is visible and easily intercepted, as demonstrated using tools like Wireshark.

## HTTPS: HTTP Over TLS

- **Definition**:
  - HTTPS = HTTP secured with **TLS** (Transport Layer Security).
  - Operates over **TCP** on port 443.
- **Process**:

  1. Resolve the domain name to an IP address.
  2. **TCP Three-Way Handshake**:
     - Same as HTTP.
  3. **TLS Session Establishment**:
     - Negotiates encryption between client and server.
  4. **Encrypted HTTP Communication**:
     - Data packets are encrypted and appear as "Application Data" in tools like Wireshark.
  5. **TCP Connection Termination**:
     - Closes the connection.

- **Security Advantage**:
  - Encrypted traffic ensures:
    - **Confidentiality**: Data cannot be read without the encryption key.
    - **Integrity**: Data remains unchanged during transmission.
    - **Authenticity**: Validates the server's identity.

## Wireshark Observations

- **HTTP Traffic**:
  - Displays plaintext, making it easy to follow requests and responses.
- **HTTPS Traffic**:
  - Appears as encrypted gibberish without access to the private key.
  - After providing the decryption key, regular HTTP traffic is visible, but encrypted.

## Key Takeaways

- **TLS Integration**:
  - Provides security without modifying underlying protocols like TCP or IP.
  - Allows HTTP to operate over TLS seamlessly.
- **Security Benefits**:
  - Protects data from interception and ensures secure web communication.

# Adding TLS to SMTP, POP3, and IMAP

## Overview

- **TLS Integration**:
  - The process of adding TLS to **SMTP**, **POP3**, and **IMAP** is similar to adding TLS to **HTTP**.
  - Secure versions of these protocols are indicated by appending an "S" to their names (e.g., SMTPS, POP3S, IMAPS).
  - Functions like HTTPS, ensuring encryption and security.

## Protocol Port Numbers

- **Insecure Versions** (Default TCP Ports):

  - **HTTP**: 80
  - **SMTP**: 25
  - **POP3**: 110
  - **IMAP**: 143

- **Secure Versions** (Over TLS):
  - **HTTPS**: 443
  - **SMTPS**: 465 and 587
  - **POP3S**: 995
  - **IMAPS**: 993

## Key Points

- **Encryption**:
  - TLS encrypts the data, ensuring confidentiality and preventing interception.
- **Consistency**:
  - Similar benefits and implementation as seen with HTTPS.
- **Other Protocols**:
  - Many protocols can be upgraded to use TLS, following the same principles for security and reliability.

## Takeaways

- TLS-secured protocols (e.g., SMTPS, POP3S, IMAPS) provide secure communication without modifying the underlying protocols.
- Encryption ensures that sensitive information (e.g., emails) is protected from unauthorized access.

# Secure Shell (SSH) Protocol Overview

## History and Development

- **TELNET Vulnerability**:
  - TELNET transmits all traffic, including login credentials, in cleartext, posing significant security risks.
- **SSH Introduction**:
  - Developed by **Tatu Ylönen** in 1995 as a secure alternative to TELNET.
  - **SSH-1**: Initial release as freeware.
  - **SSH-2**: Released in 1996 with enhanced security features.
  - **OpenSSH**: Introduced in 1999 by OpenBSD developers, now the most common SSH implementation.

## Features of OpenSSH

- **Secure Authentication**:
  - Supports various methods like passwords, public keys, and two-factor authentication.
- **Confidentiality**:
  - Encrypts all data to protect against eavesdropping.
  - Alerts users to new server keys, mitigating man-in-the-middle attacks.
- **Integrity**:
  - Ensures the exchanged data remains unaltered during transmission.
- **Tunneling**:
  - Routes other protocols through SSH, creating secure VPN-like connections.
- **X11 Forwarding**:
  - Enables the use of graphical applications on remote Unix-like systems over SSH.

## Usage

- **Command Syntax**:
  - `ssh username@hostname`
  - If the username matches the local login, you can simply use `ssh hostname`.
- **Port**:
  - TELNET operates on **port 23**, while SSH uses **port 22**.

## Example Application

- **Wireshark via SSH**:
  - Connect to a remote server using the `-X` argument to enable graphical interfaces (e.g., `ssh 192.168.124.148 -X`).
  - This allows running applications like Wireshark remotely with a graphical user interface.

## Key Takeaways

- SSH provides a secure alternative to TELNET by offering encryption, authentication, and additional capabilities.
- OpenSSH is widely adopted for its robust and open-source implementation.
- Always use SSH over TELNET for secure remote system administration.

# Secure File Transfer Protocols: SFTP vs. FTPS

## What is SFTP?

- **Definition**:
  - SFTP stands for **SSH File Transfer Protocol**, a secure method for transferring files using the SSH protocol.
- **Port**:
  - Operates on the same port as SSH: **port 22**.
- **Usage**:
  - Command: `sftp username@hostname`.
  - Common Commands:
    - `get filename` - Download a file.
    - `put filename` - Upload a file.
  - SFTP commands resemble Unix-like syntax but differ from traditional FTP commands.

## Setting Up SFTP

- SFTP functionality can be enabled by configuring the **OpenSSH server**.
- No additional software is required beyond OpenSSH for basic SFTP server setup.

---

## How Does FTPS Differ?

- **Definition**:
  - FTPS stands for **File Transfer Protocol Secure**.
  - Secures file transfers using **TLS**, akin to HTTPS.
- **Ports**:
  - FTP uses **port 21**, while FTPS typically operates on **port 990**.
- **Setup Requirements**:
  - Requires a proper **TLS certificate**.
  - Uses separate connections for control and data, which can complicate setups behind strict firewalls.

---

## Key Comparisons

| Feature         | SFTP                                                 | FTPS                                                                 |
| --------------- | ---------------------------------------------------- | -------------------------------------------------------------------- |
| **Security**    | Uses SSH for encryption and secure authentication.   | Uses TLS for encryption; requires certificates.                      |
| **Port**        | Port 22                                              | Port 990 (default) for FTPS.                                         |
| **Ease of Use** | Simple setup via OpenSSH configuration.              | More complex; requires TLS configuration and certificate management. |
| **Firewalls**   | Easier to configure, as it uses a single connection. | May face issues due to multiple connections for control/data.        |

---

## Key Takeaways

- **SFTP** is part of the SSH suite, offering straightforward and secure file transfer.
- **FTPS** relies on TLS and can be more challenging to set up and manage due to its multi-connection nature.
- Both protocols enhance security compared to plain FTP but serve different operational needs.
