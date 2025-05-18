# Windows Server Network Vulnerability Scan

**Date:** 2025-05-18  
**Scanner:** Nmap 7.95 on Kali Linux  

## 1. Objective  
Perform an initial and unauthenticated network‐level vulnerability assessment against 192.168.56.101 (Windows Server 2025 VM).

## 2. Methodology  
- TCP SYN & version detection (`-sS -sV`)  
- Run vulnerability NSE scripts (`--script=vuln`)  
- Scan ports 1–65535  

nmap -Pn -sS -sV --script=vuln -p1-65535 192.168.56.101 -oN windows_full_nmap.nmap


## 3. Findings

| Port | Service         | NSE Result               | Risk  | Recommendation                                   |
|------|-----------------|--------------------------|-------|--------------------------------------------------|
| 3389 | ms-wbt-server   | *(no vuln scripts found)*| Medium| Enforce NLA, firewall restrict, use RD Gateway   |
| 5985 | HTTPAPI/2.0     | No XSS/CSRF found        | Medium| Migrate to HTTPS (5986), lock listener to subnet|

## 4. Next Steps  
1. Run credentialed SMB & WinRM scans (have had issues initializing a openVAS greenbone scan due to issues with NVTs not being available.  
2. Harden RDP and WinRM per MS best practices.  
3. Schedule a weekly Nmap sweep to catch new exposures.

## 5. Appendix  
- Full output: `windows_full_nmap.nmap`  
- Raw data: `windows_full_nmap.xml`, `windows_full_nmap.html`
