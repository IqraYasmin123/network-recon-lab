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

Example:
```
nmap -A 192.168.1.10 -oN scans/192.168.1.10-full-scan.txt
```

## Results log

| Target IP | Open ports | Service/version | OS guess | Notes |
|-----------|------------|------------------|----------|-------|
|           |            |                  |          |       |

## Screenshot / evidence checklist

- [ ] `-sn` host discovery output
- [ ] `-sV` service detection output
- [ ] `-O` or `-A` OS detection output
- [ ] Raw output files saved in `scans/`
