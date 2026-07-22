# Network Recon & Fundamentals Lab

A self-paced lab for learning core networking concepts and practicing ethical
reconnaissance (Wireshark + Nmap) in a **virtual, isolated lab environment only**.

> ⚠️ **Scope reminder:** Only run scans/captures against systems you own or are
> explicitly authorized to test (e.g., your own VMs on a host-only/NAT network).
> Never point these tools at networks or hosts you don't have permission to test.

## Repo Structure

```
network-recon-lab/
├── README.md                  # This file
├── docs/
│   ├── networking-notes.md    # OSI/TCP-IP/ports/protocols/DNS/DHCP/HTTP notes
│   ├── ip-addressing.md       # Public vs private IP, subnetting practice
│   ├── wireshark-notes.md     # Wireshark workflow + filters cheat sheet
│   ├── nmap-notes.md          # Nmap commands + what each flag does
│   ├── attack-mapping.md      # CVE/CVSS/MITRE ATT&CK research notes
│   └── report-template.md     # Final submission report template
├── scans/                     # Save raw Nmap output here (.txt / .xml)
├── captures/                  # Save Wireshark .pcapng exports here
└── screenshots/                # Screenshots for submission
```

## Task Checklist

- [ ] Learn Networking Basics (OSI, TCP/IP, Ports, Protocols, DNS, DHCP, HTTP/HTTPS)
- [ ] Practice IP Addressing (Public vs Private, Subnetting)
- [ ] Wireshark: capture traffic, identify protocols, export a capture
- [ ] Nmap: host discovery, port scan, service detection, OS detection
- [ ] Research: pick 1 CVE from a discovered service, note its CVSS score
- [ ] Map recon activity to MITRE ATT&CK techniques
- [ ] Write final report (docs/report-template.md)

## Learning Resources

- Networking crash course: https://www.youtube.com/watch?v=qiQR5rTSshw
- Nmap tutorial: https://www.youtube.com/watch?v=4t4kBkMsDbQ
- Wireshark tutorial: https://www.youtube.com/watch?v=TkCSr30UojM
- MITRE ATT&CK: https://attack.mitre.org/
- NVD (CVE lookup): https://nvd.nist.gov/vuln/search
- CVSS calculator: https://www.first.org/cvss/calculator/3.1

## How to use this repo in VS Code

1. Open this folder in VS Code (`File > Open Folder...`).
2. Install the extensions: **Markdown All in One** and, if you like syntax
   highlighting for scan output, **Log File Highlighter**.
3. Fill in each file under `docs/` as you complete that section of the lab.
4. Drop your raw Nmap output into `scans/`, Wireshark exports into `captures/`,
   and screenshots into `screenshots/`.
5. Commit as you go (see suggested commit messages in each doc file).
