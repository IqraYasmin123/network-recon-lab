# Lab Report: Networking Basics & Ethical Reconnaissance

**Name:IQRA YASMEEN
**Date:25.07.2026
**Lab environment:** VMware Workstation, host-only network 192.168.142.0/24, VMs: Kali Linux (attacker) + Metasploitable2 (target)

## 1. Objective

The goal of this lab was to build a working understanding of core networking
concepts (OSI/TCP-IP models, ports, protocols, DNS, DHCP, HTTP/HTTPS, IP
addressing, and subnetting), and to apply that knowledge through hands-on,
ethical reconnaissance in an isolated virtual lab — using Wireshark to
capture and analyze live network traffic, and Nmap to perform host
discovery, port scanning, service/version detection, and OS fingerprinting
against a deliberately vulnerable target.

## 2. Environment Setup

- Hypervisor / VM software used: VMware Workstation
- VMs involved (attacker + target) and their IPs:
  - Kali Linux (attacker) — 192.168.142.128
  - Metasploitable2 (target) — 192.168.142.136
- Network mode: Host-only (isolated from the internet and host's real network)

## 3. Methodology

1. Installed VMware Workstation and imported/created the Kali Linux and
   Metasploitable2 virtual machines.
2. Configured both VMs' network adapters to the same host-only network to
   keep all traffic isolated from the internet and the host's real LAN.
3. Confirmed connectivity between the two VMs using `ping`.
4. Reviewed core networking concepts (OSI model, TCP/IP, ports, DNS, DHCP,
   HTTP/HTTPS) and practiced subnetting by hand.
5. Opened Wireshark on Kali, started a capture on `eth0`, then generated
   ICMP (`ping`) and HTTP (`curl`) traffic toward Metasploitable2 to
   capture real packets.
6. Applied Wireshark display filters (`icmp`, `http`) to isolate and
   examine specific protocols, and used "Follow → HTTP Stream" to view a
   full request/response exchange. Exported the capture as `capture1.pcapng`.
7. Ran a sequence of Nmap scans against Metasploitable2:
   - `nmap -sn 192.168.142.0/24` — host discovery
   - `nmap -sV 192.168.142.136` — service/version detection
   - `sudo nmap -O 192.168.142.136` — OS detection
   - `sudo nmap -A 192.168.142.136` — combined aggressive scan
8. Identified `vsftpd 2.3.4` (port 21) from the scan results as a
   deliberately vulnerable service, and researched its associated CVE and
   CVSS score.
9. Mapped the reconnaissance activities performed to relevant MITRE
   ATT&CK tactics and techniques.

## 4. Findings

### 4.1 Host Discovery

The `nmap -sn 192.168.142.0/24` scan identified 3 live hosts on the
subnet: the VMware host-only gateway (192.168.142.2), Kali
(192.168.142.128), and Metasploitable2 (192.168.142.136). See
`screenshots/` for the scan output and `scans/host-discovery.txt` for
the raw results.

### 4.2 Port Scanning / Service Detection

The `nmap -sV` scan against Metasploitable2 found 17 open TCP ports,
many running deliberately outdated and vulnerable service versions:

| Port | Service | Version |
|---|---|---|
| 21 | ftp | vsftpd 2.3.4 |
| 22 | ssh | OpenSSH 4.7p1 Debian 8ubuntu1 |
| 23 | telnet | Linux telnetd |
| 80 | http | Apache httpd 2.2.8 (Ubuntu) DAV/2 |
| 111 | rpcbind | RPC #100000 |
| 512 | exec | netkit-rsh rexecd |
| 513 | login | OpenBSD/Solaris rlogind |
| 514 | shell | tcpwrapped |
| 1099 | java-rmi | GNU Classpath grmiregistry |
| 1524 | bindshell | Metasploitable root shell |
| 2121 | ftp | ProFTPD 1.3.1 |
| 3306 | mysql | MySQL 5.0.51a-3ubuntu5 |
| 5432 | postgresql | PostgreSQL 8.3.0–8.3.7 |
| 5900 | vnc | VNC (protocol 3.3) |
| 6000 | X11 | (access denied) |
| 6667 | irc | UnrealIRCd |
| 8009 | ajp13 | Apache Jserv 1.3 |
| 8180 | http | Apache Tomcat/Coyote 1.1 |

Full raw output is saved in `scans/service-scan.txt`.

### 4.3 OS Detection

`sudo nmap -O` identified the target as running **Linux kernel
2.6.9–2.6.33**, consistent with Metasploitable2's intentionally outdated
Ubuntu 8.04 base. Raw output saved in `scans/os-scan.txt`.

### 4.4 Wireshark Capture

Traffic was captured on Kali's `eth0` interface while pinging and
`curl`-ing Metasploitable2. The capture clearly showed:
- ICMP Echo Request/Reply pairs from the `ping` command
- A full TCP three-way handshake (SYN → SYN/ACK → ACK) followed by an
  HTTP GET request and 200 OK response from the `curl` command
- Normal background broadcast traffic (ARP, MDNS, SSDP) from the host
  network, unrelated to the lab traffic itself

Screenshots of the filtered `icmp` and `http` views, and the "Follow
HTTP Stream" output, are saved in `screenshots/`. The full capture is
saved as `captures/capture1.pcapng`.

## 5. Vulnerability Research

The `vsftpd 2.3.4` service on port 21 was selected for deeper research.
This exact version corresponds to **CVE-2011-2523**: between June 30 and
July 3, 2011, the official vsftpd download archive was compromised with
a malicious backdoor. Logging in with `:)` as the username triggers the
backdoor, opening a command shell on port 6200/tcp with no valid
credentials required.

- **CVSS v3 Base Score:** 9.8 (Critical) — `AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H`
- **CVSS v2 Base Score:** 10 (Critical)

This score reflects that the vulnerability is remotely exploitable
(Network vector), trivial to carry out (Low complexity), requires no
credentials or user interaction, and results in full compromise of
confidentiality, integrity, and availability. Full details are in
`docs/attack-mapping.md`.

## 6. MITRE ATT&CK Mapping

| Activity | ATT&CK Tactic | ATT&CK Technique |
|---|---|---|
| Ping sweep / host discovery | Reconnaissance / Discovery | T1018 – Remote System Discovery |
| Port scanning | Reconnaissance | T1595 – Active Scanning |
| Service/version detection | Discovery | T1046 – Network Service Discovery |
| OS fingerprinting | Discovery | T1082 – System Information Discovery |
| Exploiting the vsftpd backdoor to get a shell | Initial Access | T1190 – Exploit Public-Facing Application |
| Using the backdoor's shell to run further commands | Execution | T1059 – Command and Scripting Interpreter |

## 7. Conclusion

This lab gave hands-on experience with the full reconnaissance workflow
a penetration tester follows before any exploitation begins: mapping a
network, identifying live hosts, enumerating open ports and services,
fingerprinting the OS, and cross-referencing findings against known
vulnerabilities. The most valuable takeaway was seeing how directly a
single piece of banner information — a service name and version number
— can lead straight to a critical, pre-documented vulnerability with a
CVSS score of 9.8, without needing to discover anything new. This
mirrors real-world penetration testing, where the recon phase often
determines the entire attack path before a single exploit is ever run.

## Appendix: File Index

| File | Description |
|---|---|
| `scans/*.txt` | Raw Nmap output |
| `captures/*.pcapng` | Wireshark capture export |
| `screenshots/*.png` | Supporting screenshots |