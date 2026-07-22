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

_(Fill in as you go — list each protocol you spotted, what it was doing,
and a one-line note on why it matters.)_

| Protocol | What I saw | Notes |
|----------|------------|-------|
|          |            |       |

## Screenshot checklist

- [ ] Capture running / packet list view
- [ ] A filtered view (e.g., `dns` or `http`)
- [ ] A "Follow TCP Stream" window
- [ ] Confirmation of exported `.pcapng` file
