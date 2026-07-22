# Vulnerability Research & ATT&CK Mapping

## Step 1 — Pick a service from your Nmap results

From your `-sV` scan, pick one service + version (e.g., an old vsftpd,
Apache, or OpenSSH build) that looks worth researching.

- Service/version found: `___________________`
- Host it was found on: `___________________`

## Step 2 — Look up a related CVE

Search https://nvd.nist.gov/vuln/search for that service/version.

- CVE ID: `___________________`
- Short description: `___________________`
- CVSS base score: `___________________`
- CVSS vector string: `___________________`
- What the vector string means (attack vector, complexity, privileges
  required, impact): `___________________`

## Step 3 — Map your recon activity to MITRE ATT&CK

Reference: https://attack.mitre.org/

| Activity | ATT&CK Tactic | ATT&CK Technique |
|---|---|---|
| Ping sweep / host discovery | Reconnaissance / Discovery | T1018 – Remote System Discovery |
| Port scanning | Reconnaissance | T1595 – Active Scanning |
| Service/version detection | Discovery | T1046 – Network Service Discovery |
| OS fingerprinting | Discovery | T1082 – System Information Discovery |

_(Adjust/expand this table based on what you actually did — the IDs above
are the common ones for basic Nmap recon, but double-check them against
the current ATT&CK site since technique numbering does get revised.)_

## Reflection

_(2–3 sentences: how would a real attacker use this recon info as a next
step? What would a defender look for in logs/IDS to catch this kind of
scanning?)_
