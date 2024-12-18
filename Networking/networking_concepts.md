# OSI Model

## Layer 1: Physical Layer

Examples: cables, antennas, WiFi bands (2.4GHz, 5GHz and 6GHz).

## Layer 2: Data Link Layer

The data link layer represents the protocol that enables data transfer on the same network. It describes the agreement between different systems on a network and how they will communicate.

Examples: Ethernet (802.3) and WiFi (802.11).

Ethernet and WiFi addresses are 6 bytes (called the MAC address).

## Layer 3: Network Layer

The network layer is concerned with sending data between different networks. It handles logical addressing and routing.

Examples: Internet Protocol (IP), Internet Control Message Protocol (ICMP), and VPN protocols such as IPSec and SSL/TLS VPN.

## Layer 4: Transportation Layer

Enables end-to-end communication between running application on different hosts. A web browser is connected to a web site of the transporation layer. It can support functions like flow control, segmentation, and error correction.

Examples: Transmission Control Protocol (TCP) and User Datagram Protocol (UDP).

## Layer 5: Session Layer

The session layer is responsible for establishing, maintaining, and synchronising communication between applications running on different hosts.

Examples: Network File System (NFS) and Remote Procedure Call (RPC).

## Layer 6: Presentation Layer

The presentation layer ensures the data is delivered in a form the application layer can understand. It handles encoding, compression, and encryption.

Examples: Unicode, MIME, JPEG, PNG, MPEG

## Layer 7: Application Layer

The application layer provides network services directly to end-user applications. A browser would use HTTP.

Examples: HTTP, FTP, DNS, POP3, SMTP, and IMAP.

# TCP/IP Model

The TCP/IP model is an implemented model.

- Application Layer - layers 5, 6, and 7.
- Transport Layer - layer 4.
- Internet Layer - layer 3.
- Link Layer - layer 2.

# IP Addresses and Subnets

IP addresses are composed of 32 bits, or 4 x 8 bit octets.

192.168.1.0 - often the network address

192.168.1.255 - broadcast address; sending here will broadcast all hosts on a network.

```bash
`ipconfig`                              // for Windows cli
`ifconfig` or `ip address show`         // for linux/unix
```

A subnet mask may be written either in full form such as `255.255.255.0` or `/24`. In abreviated form, it would be found at the end of a IP address (`192.168.55.65/24`). In this case, it means that the leftmost 24 bits in the IP address do not change across the network. Addresses across the network would range from 192.168.55.1 - 192.168.55.255.

## Private Addresses

Private Addresses includes addresses in the following three IP address ranges:

- 10.0.0.0 - 10.255.255.255 (10/8)
- 172.16.0.0 - 172.31.255.255 (172.16/12)
- 192.168.0.0 - 192.168.255.255 (192.168/16)

Private addresses cannot be reached from the outside world. In order for private IP addresses to access the Internet, the router must have a public IP address and must support Network Address Translation (NAT).

## Routing

A router forwards data packets to the proper network. It functions at layer 3. It inspects the IP address and forwards the packet to the best network (router) so the packet gets closer to its destination.

# UDP and TCP

## UDP

User Datagram Protocol is connectionless that operates at layer 4. It does not establish a connection, nor does it provide any mechanism to know whether a packet arrived. Port (numbers) are the mechanism that determines the sending/receiving process.

## TCP

Transmission Control Protocol is a connection-oriented transport protocol. A TCP connection is required to be established before data is sent.

Each data octet has a sequence number, making it easy to identify lost or duplicate packets. The receiver acknowledges reception with a acknowledgement number.

TCP uses the three-way handshake:

1. SYN Packet - connection is initiated by sending a SYN packet to a server. It contains the client's initial sequence number.
2. SYN-ACK Packet - server responds with a SYN-ACK packet, adding the initial sequence number randomly chosen by the server.
3. ACK Packet - ACK packet acknowledges reception of SYN-ACK packet.

## Encapsulation

Every layer adds a header (and sometimes a trailer) to the received unit of data.

- Application layer - formats data according to protocol used.
- Transport layer - Adds header information and creates the TCP segment or UDP datagram.
- Network layer - adds IP header to create packet.
- Data link layer - adds header and trailer, creating a frame.

## Telnet

The `TELNET` protocol is used for remote terminal connection. It can be used to connect to any server listening on a TCP port number.

`telnet ip_address port_number` // telnet 10.10.108.83 7

To get a HTTP page via port 80:

```bash
telnet 10.10.108.83 80                              // establish connection
...

GET / HTTP/1.1                                      // issue command
Host: telnet.thm                                    // identify host where anything goes
                                                    // press enter twice
```

`GET /file.html` may also work depending on type of server.
