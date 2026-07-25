# Wireshark — Workflow & Cheat Sheet

## Workflow

1. Open Wireshark, select the active network interface.
2. Click the shark-fin icon (or Ctrl+E) to start capturing.
3. Generate some traffic in another window: browse a site, `ping 8.8.8.8`,
   do a DNS lookup (`nslookup example.com`).
4. Stop the capture (red square icon).
5. Apply a display filter (see below) to isolate what you're interested in.
6. Right-click a packet → **Follow → TCP Stream** to see a full conversation
   reconstructed.
7. Export: **File → Export Specified Packets...** → save as `.pcapng` into
   `captures/`.

## Useful display filters

| Filter                | Shows                                  |
|------------------------|------------------------------------------|
| `http`                 | HTTP requests/responses                |
| `dns`                  | DNS queries and responses               |
| `tcp.port == 443`      | Traffic on port 443 (HTTPS)             |
| `icmp`                 | Ping (ICMP) traffic                     |
| `ip.addr == 192.168.1.5` | Traffic to/from a specific host       |
| `tcp.flags.syn == 1 && tcp.flags.ack == 0` | TCP SYN packets (connection attempts) |

## Protocols identified in my capture

| Protocol | What I saw | Notes |
|----------|------------|-------|
| ICMP | 4 Echo Request/Reply pairs from `ping 192.168.142.136` (Kali → Metasploitable2) | Confirms basic reachability between the two VMs before any port-level traffic |
| TCP | Full three-way handshake (SYN → SYN/ACK → ACK) on port 80, followed by a graceful close (FIN/ACK) | Shows a TCP connection being established and torn down before any HTTP data is sent |
| HTTP | `GET / HTTP/1.1` request from Kali, `HTTP/1.1 200 OK` response from Metasploitable2's Apache server | "Follow HTTP Stream" showed the full Metasploitable2 welcome page HTML in the response body |
| ARP | Broadcast "Who has X? Tell Y" requests between the VMs | Normal address resolution — MAC addresses being resolved for the IPs before communication |
| MDNS / SSDP | Background broadcasts originating from the host machine (192.168.142.1) | Unrelated to the lab traffic itself — Windows host network service discovery chatter picked up because it shares the host-only network |

## Screenshot checklist

- [x] Capture running / packet list view
- [x] A filtered view (`icmp`)
- [x] A filtered view (`http`)
- [x] A "Follow HTTP Stream" window
- [x] Confirmation of exported `.pcapng` file