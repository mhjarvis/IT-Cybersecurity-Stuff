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

# Nmap: Controlling Scan Speed and Timing

## Timing Templates

- **Purpose**: Adjust the speed of scans to evade Intrusion Detection Systems (IDS) or adapt to network conditions.
- **Command**: `nmap -T<0-5> [target]`
  - **T0 (Paranoid)**: Slowest, waits several minutes between probes. Ideal for evading detection.
  - **T1 (Sneaky)**: Slower timing, ~15 seconds between probes.
  - **T2 (Polite)**: Moderate, ~0.4 seconds between probes. Reduces network load.
  - **T3 (Normal)**: Default setting, balances speed and reliability.
  - **T4 (Aggressive)**: Faster scans, suitable for reliable and fast networks.
  - **T5 (Insane)**: Fastest but risks packet loss and detection by IDS.

### Timing Examples

| **Timing** | **Total Duration**     |
| ---------- | ---------------------- |
| `T0`       | 9.8 hours              |
| `T1`       | 27.53 minutes          |
| `T2`       | 40.56 seconds          |
| `T3`       | 0.15 seconds (default) |
| `T4`       | 0.13 seconds           |

---

## Parallelism Options

- **Command**:
  - `--min-parallelism <numprobes>`
  - `--max-parallelism <numprobes>`
- **Description**: Controls the number of active port probes for a host group.
  - If the network is **slow**, probes reduce to one.
  - If the network is **fast**, probes can scale to several hundred.

---

## Rate Options

- **Command**:
  - `--min-rate <number>`
  - `--max-rate <number>`
- **Description**: Sets the minimum/maximum number of packets sent per second.
  - Rate applies to the entire scan, not individual hosts.
  - Useful for fine-tuning scan performance in varying network conditions.

---

## Host Timeout

- **Command**: `--host-timeout <time>`
- **Description**: Sets the maximum duration to wait for responses from a target host.
  - Helpful for skipping slow hosts and optimizing scan time.

---

## Summary Table of Key Options

| **Option**                                | **Purpose**                                       |
| ----------------------------------------- | ------------------------------------------------- |
| `-T<0-5>`                                 | Timing template: control scan speed.              |
| `--min-parallelism` / `--max-parallelism` | Minimum and maximum number of active probes.      |
| `--min-rate` / `--max-rate`               | Minimum and maximum rate of packets (per second). |
| `--host-timeout`                          | Maximum duration to wait for a response.          |

For more details, refer to [Nmap's official documentation](https://nmap.org).

# Nmap: Verbosity, Debugging, and Saving Scan Reports

## Verbosity and Debugging

### Verbose Output (`-v`)

- **Purpose**: Provides real-time updates during a scan.
- **Usage**: Add `-v` to your Nmap command for basic verbosity.
  - Example: `nmap -v <target>`
- **Levels**: Increase verbosity by adding more "v"s (e.g., `-vv`, `-vvvv`) or by specifying the level directly (e.g., `-v2`, `-v4`).
  - Real-time adjustment: Press `v` during an active scan to increase verbosity.

### Debugging Output (`-d`)

- **Purpose**: Displays in-depth details about the scan process for troubleshooting.
- **Usage**: Add `-d` for debugging-level output.
  - Example: `nmap -d <target>`
- **Levels**: Increase debugging output by adding more "d"s (e.g., `-dd`, `-ddd`) or specifying the level directly (e.g., `-d3`, `-d9`).
  - Maximum level: `-d9` (thousands of lines of debug data).

---

## Saving Scan Reports

Nmap offers several output formats to save scan results:

- **Normal Output (`-oN <filename>`)**: Human-readable format.
  - Example: `nmap -oN scan.txt <target>`
- **XML Output (`-oX <filename>`)**: Machine-readable XML format.
  - Example: `nmap -oX scan.xml <target>`
- **Grepable Output (`-oG <filename>`)**: Output designed for use with `grep` or `awk`.
  - Example: `nmap -oG scan.gnmap <target>`
- **All Formats (`-oA <basename>`)**: Saves in all three formats with the base name provided.
  - Example: `nmap -oA scan <target>`
  - Output: Produces files `scan.nmap`, `scan.xml`, and `scan.gnmap`.

---

## Summary Table

| **Option**  | **Explanation**                                 |
| ----------- | ----------------------------------------------- |
| `-v`, `-vv` | Verbose output; real-time scan updates.         |
| `-d`, `-d9` | Debugging output; detailed internal processes.  |
| `-oN`       | Save as normal (human-readable) output.         |
| `-oX`       | Save as XML (machine-readable) output.          |
| `-oG`       | Save as grepable output for further processing. |
| `-oA`       | Save in all major formats.                      |

---

### Example Command:

```bash
nmap -v -oA scan_results <target>
```

# Summary of Nmap Features and Usage

## Key Takeaways

- **Live Host Discovery**: Learn to identify active devices on any network.
- **Port Scanning**: Understand and apply various types of scans to find open ports and services.
- **Service Version Detection**: Use Nmap to reveal the versions of services running on open ports.
- **Scan Timing**: Optimize scans by adjusting timing templates and controlling probe rates.
- **Report Formats**: Save scan results in multiple formats for analysis.

---

## Importance of Running Nmap with `sudo`

- Running with **sudo** provides full access to Nmap's features, such as:
  - TCP SYN Scan (`-sS`): Requires root privileges to craft raw packets.
  - Non-root users default to TCP Connect Scan (`-sT`), which is less efficient.

---

## Nmap Options Reference Table

| **Category**          | **Option**                  | **Description**                                             |
| --------------------- | --------------------------- | ----------------------------------------------------------- |
| **Host Discovery**    | `-sL`                       | List scan – lists targets without scanning.                 |
|                       | `-sn`                       | Ping scan – discovers hosts without port scanning.          |
| **Port Scanning**     | `-sT`                       | TCP Connect Scan – completes the three-way handshake.       |
|                       | `-sS`                       | TCP SYN Scan – sends only the SYN packet (requires `sudo`). |
|                       | `-sU`                       | UDP Scan – checks for open UDP ports.                       |
|                       | `-F`                        | Fast mode – scans the 100 most common ports.                |
|                       | `-p[range]`                 | Specifies a port range; `-p-` scans all ports.              |
|                       | `-Pn`                       | Treats all hosts as online, bypassing host discovery.       |
| **Service Detection** | `-sV`                       | Detects versions of services running on open ports.         |
|                       | `-O`                        | OS detection.                                               |
|                       | `-A`                        | Comprehensive detection: OS, versions, and other details.   |
| **Timing**            | `-T<0-5>`                   | Timing templates: 0 (paranoid) to 5 (insane).               |
|                       | `--min-rate` / `--max-rate` | Minimum/maximum rate of probes per second.                  |
|                       | `--host-timeout`            | Max wait time for a target host.                            |
| **Output**            | `-oN <filename>`            | Normal (human-readable) output.                             |
|                       | `-oX <filename>`            | XML output for machine processing.                          |
|                       | `-oG <filename>`            | Grepable output for `grep`/`awk`.                           |
|                       | `-oA <basename>`            | Saves output in all formats (normal, XML, grepable).        |

---

### Recommended Learning Path

- Nmap is a powerful tool with many features. Beyond the basics covered here, further learning can be pursued in the **Network Security module**, which includes four dedicated rooms to explore advanced Nmap functionalities.

For more in-depth details, visit the [official Nmap documentation](https://nmap.org/docs.html).
