## Networking Basics — Notes

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

Seeing the TCP three-way handshake actually happen in a Wireshark
capture (SYN → SYN/ACK → ACK, packets 31–33 in my capture) made the
concept click much more than reading about it — it's easy to read
"TCP is connection-oriented" as an abstract fact, but watching the
literal handshake packets before any HTTP data was exchanged showed
why TCP is considered reliable: the connection is fully established
and acknowledged by both sides before a single byte of the actual
request is sent.

Running the Nmap scans also clarified the port ranges in a very
concrete way — seeing FTP on 21, SSH on 22, and HTTP on 80 all show
up exactly where the "well-known ports" table says they should be
made the 0–1023 range feel like a real, checkable fact rather than
just something to memorize.

One detail I hadn't fully appreciated before this lab: UDP's lack of a
handshake isn't just "less reliable" — it's also *why* it's used for
things like DHCP and DNS, where speed matters more than guaranteed
delivery, and the application itself can retry if a request is lost.