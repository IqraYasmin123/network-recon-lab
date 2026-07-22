# Networking Basics — Notes

## OSI Model (7 layers, top → bottom)

| # | Layer        | Examples                     |
|---|--------------|-------------------------------|
| 7 | Application  | HTTP, DNS, FTP, SMTP          |
| 6 | Presentation | TLS/SSL, encoding, encryption |
| 5 | Session      | Session establishment/teardown|
| 4 | Transport    | TCP, UDP                      |
| 3 | Network      | IP, ICMP, routing              |
| 2 | Data Link    | Ethernet, MAC addresses, switches |
| 1 | Physical     | Cables, radio, electrical signals |

Mnemonic: **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing.

## TCP/IP Model (4 layers)

Application → Transport → Internet → Link. Maps roughly onto OSI but
collapses layers 5–7 into "Application" and layers 1–2 into "Link".

- **TCP**: connection-oriented, reliable, ordered. 3-way handshake:
  `SYN → SYN/ACK → ACK`.
- **UDP**: connectionless, no handshake, no delivery guarantee, lower overhead
  (used for DNS queries, streaming, DHCP, etc.)

## Ports

- **0–1023**: well-known (22 SSH, 23 Telnet, 25 SMTP, 53 DNS, 80 HTTP, 443 HTTPS)
- **1024–49151**: registered
- **49152–65535**: dynamic/ephemeral (used for outbound client connections)

## Protocols to know

- **DNS** (UDP/TCP 53) — resolves domain names to IP addresses.
- **DHCP** (UDP 67/68) — auto-assigns IP configuration to hosts on a network.
- **HTTP** (TCP 80) — unencrypted web traffic.
- **HTTPS** (TCP 443) — HTTP wrapped in TLS for encryption/integrity.

## Notes from my own research

_(Fill in anything from the video/your own reading that clarified a concept
for you — e.g., a specific analogy that made subnetting click, or a detail
about the TCP handshake you hadn't seen before.)_
