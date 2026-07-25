# Vulnerability Research & ATT&CK Mapping

## Step 1 — Pick a service from your Nmap results

From your `-sV` scan, pick one service + version (e.g., an old vsftpd,
Apache, or OpenSSH build) that looks worth researching.

- Service/version found: `vsftpd 2.3.4`
- Host it was found on: `192.168.142.136 (Metasploitable2)`

## Step 2 — Look up a related CVE

Search https://nvd.nist.gov/vuln/search for that service/version.

- CVE ID: `CVE-2011-2523`
- Short description: `vsftpd 2.3.4 downloaded between June 30 and July 3, 2011 contained a malicious backdoor. Logging in with ":)" as the username triggers the backdoor, opening a command shell on port 6200/tcp with no valid credentials needed. The FTP server binary itself had been tampered with on the official download site — this was a supply-chain compromise, not a coding bug.`
- CVSS base score: `9.8 (CVSS v3, Critical) / 10 (CVSS v2, Critical)`
- CVSS vector string: `CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H`
- What the vector string means (attack vector, complexity, privileges
  required, impact): `AV:N means the attack can be carried out remotely over the network. AC:L means it requires no special conditions and is easy to exploit. PR:N means the attacker needs no prior privileges or valid account. UI:N means no victim interaction is required. C:H/I:H/A:H means full impact on confidentiality, integrity, and availability — a successful attacker gets complete control of the system.`
## Step 3 — Map your recon activity to MITRE ATT&CK

Reference: https://attack.mitre.org/

| Activity | ATT&CK Tactic | ATT&CK Technique |
|---|---|---|
| Ping sweep / host discovery | Reconnaissance / Discovery | T1018 – Remote System Discovery |
| Port scanning | Reconnaissance | T1595 – Active Scanning |
| Service/version detection | Discovery | T1046 – Network Service Discovery |
| OS fingerprinting | Discovery | T1082 – System Information Discovery |
| Exploiting the vsftpd backdoor to get a shell | Initial Access | T1190 – Exploit Public-Facing Application |
| Using the backdoor's shell to run further commands | Execution | T1059 – Command and Scripting Interpreter |
## Reflection

_(2–3 sentences: how would a real attacker use this recon info as a next
step? What would a defender look for in logs/IDS to catch this kind of
scanning?)_
