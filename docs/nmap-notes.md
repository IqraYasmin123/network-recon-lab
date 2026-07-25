# Nmap — Commands & Notes

> ⚠️ Only run against hosts/networks you own or are authorized to test —
> e.g., VMs on your own host-only/NAT virtual lab network.

## Core commands

| Command | Purpose |
|---|---|
| `nmap -sn 192.168.1.0/24` | **Host discovery** — ping sweep, finds live hosts without port scanning |
| `nmap -sV <target-ip>` | **Service/version detection** — identifies what's running on open ports |
| `nmap -O <target-ip>` | **OS detection** — fingerprints the target's operating system (needs elevated privileges) |
| `nmap -A <target-ip>` | **Aggressive scan** — combines OS detection, version detection, script scanning, and traceroute |

## Suggested scan order

1. `nmap -sn 192.168.1.0/24` — find what's alive on the lab subnet.
2. `nmap -sV <target-ip>` on each live host — see open ports + services.
3. `nmap -O <target-ip>` or `nmap -A <target-ip>` on the interesting host(s).
4. Save output: append `-oN scans/<target>-scan.txt` (normal) or
   `-oX scans/<target>-scan.xml` (XML, machine-parseable) to any command.

Example: `nmap -A 192.168.1.10 -oN scans/192.168.1.10-full-scan.txt`

## Results log

| Target IP | Open ports | Service/version | OS guess | Notes |
|-----------|------------|------------------|----------|-------|
| 192.168.142.136 | 21, 22, 23, 80, 111, 512, 513, 514, 1099, 1524, 2121, 3306, 5432, 5900, 6000, 6667, 8009, 8180 | vsftpd 2.3.4, OpenSSH 4.7p1, Apache 2.2.8, MySQL 5.0.51a, PostgreSQL 8.3.0-8.3.7, UnrealIRCd, Apache Tomcat 5.5, and others | Linux 2.6.9 – 2.6.33 | Port 1524 identified by Nmap itself as "Metasploitable root shell." Port 21 (vsftpd 2.3.4) has a known backdoor — see `docs/attack-mapping.md` for CVE-2011-2523 details. |

## Screenshot / evidence checklist

- [x] `-sn` host discovery output
- [x] `-sV` service detection output
- [x] `-O` or `-A` OS detection output
- [x] Raw output files saved in `scans/`