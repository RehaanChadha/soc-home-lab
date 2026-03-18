# SOC Home Lab with Wazuh

## Project Overview
This project is a self-built Security Operations Center (SOC) home lab designed to simulate real-world cyber attacks and monitor them using Wazuh SIEM.

The lab includes:
- Ubuntu Server running Wazuh SIEM
- Windows machine as the victim endpoint
- Kali Linux as the attacker machine

## Objectives
- Build a working SOC lab
- Ingest and analyze Windows security logs
- Simulate attacks from Kali Linux
- Detect authentication abuse and suspicious activity in Wazuh
- Document detection gaps and lessons learned

## Lab Architecture
Kali Linux (Attacker) → Windows (Victim) → Ubuntu Wazuh SIEM (Monitoring)

## Tools Used
- Wazuh
- Ubuntu Server
- Windows
- Kali Linux
- Hydra
- Nmap
- UTM

## Attack Simulations
### 1. Failed Login / Brute Force Simulation
A brute-force style authentication attack was simulated against the Windows machine. This produced authentication failure events in Wazuh and triggered MITRE ATT&CK mappings related to brute force and account access.

### 2. Nmap Reconnaissance
Nmap scans were executed from Kali against the Windows machine. Detection was limited, which highlighted a visibility gap in host-based monitoring.

## Key Results
- Wazuh SIEM deployed successfully
- Windows agent connected successfully
- Security logs ingested and visualized
- Authentication failures detected
- MITRE ATT&CK mappings displayed in the dashboard
- Nmap scan detection was limited by default logging

## Key Security Insight
This lab showed that host-based SIEM tools like Wazuh are strong at detecting endpoint events such as failed logins, but weaker at detecting pure network reconnaissance without additional network logging or IDS tools.

## Future Improvements
- Add Sysmon to Windows for richer telemetry
- Add Suricata or Zeek for network-level detection
- Create custom Wazuh rules
- Improve visualization and alert tuning

## Screenshots
Add screenshots in the `screenshots/` folder and reference them here if needed.

## Author
Rehaan
