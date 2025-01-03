Nmap (Network Mapper) is a open-source tool used for network discovery and security auditing. It also assists in the exploration of network hosts and services, providing information about open ports, operating systems, and other details.

# Nmap: Discovering Live Hosts

## Specifying Targets in Nmap

Nmap provides multiple ways to define scanning targets:

1. **IP Range (`-`)**: Scan a specific range of IPs.
   - Example: `192.168.0.1-10` scans from `192.168.0.1` to `192.168.0.10`.
2. **IP Subnet (`/`)**: Scan an entire subnet.
   - Example: `192.168.0.1/24` covers `192.168.0.0-255`.
3. **Hostname**: Use a hostname as the target.
   - Example: `example.thm`.

---

## Local Network Scanning

- **Definition**: Directly connected networks (Ethernet or WiFi).
- **Command Example**: `nmap -sn 192.168.66.0/24`
- **Output**:
  - Displays live hosts with their IPs and MAC addresses.
  - Example:
    ```
    Nmap scan report for 192.168.66.1
    Host is up (0.0069s latency).
    MAC Address: 44:DF:65:D8:FE:6C (Unknown)
    ```
- **How It Works**:
  - Sends ARP requests to identify devices.
  - Responding devices are marked as "Host is up".

---

## Remote Network Scanning

- **Definition**: Networks separated by one or more routers.
- **Command Example**: `nmap -sn 192.168.11.0/24`
- **Output**:
  - Identifies live hosts without ARP requests.
  - Example:
    ```
    Nmap scan report for 192.168.11.1
    Host is up (0.018s latency).
    ```
- **Mechanism**:
  - Uses ICMP echo (ping) requests and TCP packets to detect live hosts.

---

## Advanced Target Discovery Options

- **Custom Port Probes**:
  - `-PS[portlist]`: TCP SYN discovery.
  - `-PA[portlist]`: TCP ACK discovery.
  - `-PU[portlist]`: UDP discovery.
- **List Scan**:
  - Command: `nmap -sL 192.168.0.1/24`
  - Output: Lists all targets without scanning.

---

## Key Notes

- Use `sudo` or root privileges for advanced scans.
- `-sn`: A lightweight option to discover live hosts without scanning services.
- To scan services on live hosts, use a more "noisy" scan (explored later).

---

## Getting Started

1. Start the AttackBox.
2. Open the terminal and experiment with the above commands.
3. Use `nmap -sL` to confirm targets before full scans.

---

# Nmap: Discovering Network Services

## Introduction to Network Services

A **network service** is any process listening for incoming connections on a specific TCP or UDP port. Common examples:

- **Web servers**: Listen on TCP ports 80 (HTTP) and 443 (HTTPS).
- **DNS servers**: Use UDP (and sometimes TCP) on port 53.

TCP and UDP each have 65,535 ports, requiring tools like Nmap to identify which ports have active services.

---

## TCP Port Scanning Methods

### 1. **Connect Scan** (`-sT`)

- **What it does**: Attempts to establish a full TCP three-way handshake with target ports.
- **How it works**:
  1. Sends a SYN packet.
  2. Waits for a SYN-ACK response from open ports.
  3. Completes the handshake and then tears down the connection with a RST-ACK packet.
- **Usage**: `nmap -sT <target>`
- **Example Output**:

- **Note**: Reliable but noisy as it generates logs on the target system.

### 2. **SYN Scan (Stealth)** (`-sS`)

- **What it does**: Sends only the initial SYN packet and awaits a SYN-ACK response from open ports.
- **Why use it**: Stealthier than connect scans; doesn't complete the three-way handshake.
- **Usage**: `nmap -sS <target>`
- **Output Example**:
- Open port: SYN-ACK response.
- Closed port: RST packet from the target.
- **Ideal for**: Minimizing logs on the target system.

---

## UDP Port Scanning

### UDP Scan (`-sU`)

- **What it does**: Sends UDP packets to target ports and waits for responses.
- **Challenges**:
- No direct connection like TCP; depends on responses (or lack thereof).
- May trigger ICMP "destination unreachable" responses for closed ports.
- **Usage**: `nmap -sU <target>`
- **Output Example**:

---

## Limiting Scans: Customizing Port Ranges

### Options:

1. **Fast Mode** (`-F`): Scans the 100 most common ports for a quicker assessment.

- Example: `nmap -F <target>`

2. **Custom Port Range** (`-p[range]`): Defines specific ports to scan.

- Examples:
  - `-p10-1024`: Scans ports 10 through 1024.
  - `-p-`: Scans all ports (equivalent to `-p1-65535`).

---

## Summary Table

| Option      | Description                                           |
| ----------- | ----------------------------------------------------- |
| `-sT`       | TCP connect scan – completes three-way handshake      |
| `-sS`       | TCP SYN scan – partial handshake for stealth scanning |
| `-sU`       | UDP scan – identifies services on UDP ports           |
| `-F`        | Fast mode – scans the 100 most common ports           |
| `-p[range]` | Defines specific port range(s) to scan                |

---

## Practical Exercises

1. **TCP Connect Scan**: `nmap -sT <target>`
2. **TCP SYN Scan**: `nmap -sS <target>`
3. **UDP Scan**: `nmap -sU <target>`
4. **Scan All Ports**: `nmap -p- <target>`
5. **Fast Scan**: `nmap -F <target>`

Start scanning and analyze the results to understand service configurations and potential vulnerabilities.

# Nmap: Detection and Scanning Options

## OS Detection

- **Command**: `nmap -sS -O [target]`
- Description: Enables Nmap's OS detection feature. It analyzes various indicators to estimate the target's operating system.
- Example Insight:
  - Detected OS: Linux 4.x or 5.x
  - More specific details: Linux versions between 4.15 and 5.8 (actual version: 5.15).
- Notes:
  - OS detection relies on Nmap's database of fingerprints.
  - While highly accurate, it’s not flawless.

---

## Service and Version Detection

- **Command**: `nmap -sS -sV [target]`
- Description: Identifies the services running on open ports and their version details.
- Example Insight:
  - Detected service: OpenSSH 8.9p1 Ubuntu (Protocol 2.0)
  - Indicates the software version and additional details like OS.
- Benefit: Saves time by combining service and version detection into a single scan.

---

## Combining Features

- **Command**: `nmap -A [target]`
- Description: Activates a suite of features, including:
  - OS detection (`-O`)
  - Service/version detection (`-sV`)
  - Traceroute
  - And other advanced scanning features.

---

## Forcing Scans on Non-Responsive Hosts

- **Command**: `nmap -Pn [target]`
- Description: Skips the host discovery phase, treating all targets as online.
- Use Case: Ensures port scanning even when a target doesn’t respond to pings (e.g., ICMP requests blocked).

---

## Summary Table of Key Options

| **Option** | **Purpose**                                                |
| ---------- | ---------------------------------------------------------- |
| `-O`       | Enables OS detection.                                      |
| `-sV`      | Detects services and their versions on open ports.         |
| `-A`       | Combines `-O`, `-sV`, traceroute, and additional features. |
| `-Pn`      | Scans hosts marked as down during host discovery.          |

For detailed information, refer to [Nmap's official documentation](https://nmap.org).
