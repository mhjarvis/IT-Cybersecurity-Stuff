# Nmap

`ARP` - protocol used to send a frame to the broadcase address on the network segment and asking the computer with a specific IP address to respond by providing its MAC address. On Ethernet and WiFi, you need to know the MAC address of any system before talking to them (why you use a ARP request). The MAC address is necessary for the link-layer header. Nmap sends `ARP` requests to all target computers, and those online should send a ARP reply back.

`ICMP` - ping using Type 8 (echo) and Type 0 (echo reply). Many firewalls block `ICMP` echo. An `ARP` request will precede the `ICMP` request.

`TCP` or `UDP` - scanner can send specially-crafted packets to common `TCP` or `UDP` ports to check whether the target will respond. Effective if `ICMP Echo` is blocked. A SYN packet can be sent (to port 80 by default) and should receive a SYN/ACK response.

`UDP` packets will not generate a reply from open ports, BUT, if the port is closed, you will get a ICMP Type 3, Code 3 packet back.

- When a `privileged user` tries to scan targets on a local network (Ethernet), Nmap uses ARP requests. A privileged user is root or a user who belongs to sudoers and can run sudo.
- When a `privileged user` tries to scan targets outside the local network, Nmap uses ICMP echo requests, TCP ACK (Acknowledge) to port 80, TCP SYN (Synchronize) to port 443, and ICMP timestamp request.
- When an `unprivileged` user tries to scan targets outside the local network, Nmap resorts to a TCP 3-way handshake by sending SYN packets to ports 80 and 443.

```bash
`nmap -sL TARGETS`                      // shows list of hosts nmap will scan (without scanning them)
`nmap -sL -n TARGETS`                   // quicker, shows hosts / number of hosts

`nmap -sn TARGETS`                      // discover online hosts without port-scanning the live systems

`-R`                                    // option for reverse-DNS lookup for all hosts

***** ARP *****
`nmap -PR -sn TARGETS`                  // only perform ARP scan without port-scanning
                                        // -PR indicates you only want a ARP scan

***** ICMP *****
`nmap -PE TARGETS`                      // ICMP echo request to discover live hosts
`nmap -PE -sn TARGETS`                  // ICMP echo request without port scan

`nmap -PP -sn TARGETS`                  // send timestamp request (ICMP Type 13)
`nmap -PM -sn TARGETS`                  // send address mask query (ICMP Type 17)

***** TCP *****
`nmap -PS TARGETS`                      // send TCP SYN ping
`nmap -PS21 TARGETS`                    // send TCP SYN ping on port 21
`nmap -PS21-25 TARGETS`                 // send TCP SYN ping on ports 21 - 25
`nmap -PS80, 443, 8080 TARGETS`         // send TCP SYN ping on ports 80, 443, 8080

`nmap -PA TARGETS`                      // sends a packet with ACK flag set; must be privileged user
                                        // unprivileged user will complete three-way handshake
                                        // should receive a packet back with RST flag set

***** UDP *****
`nmap -PU TARGETS`                      // send UDP packet; will send to a uncommon UDP port for response
```
